<template>
  <!--
    级联选择器根容器
    bem() 生成类名 "z-cascader"
  -->
  <view :class="bem()">

    <!-- ==================== 标题栏 ==================== -->
    <template v-if="props.showHeader">
      <view :class="bem('header')">
        <!-- 标题区域：优先使用 title 插槽，否则显示 props.title -->
        <view :class="bem('title')">
          <template v-if="instance.slots.title">
            <slot name="title"></slot>
          </template>
          <template v-else>
            {{ props.title }}
          </template>
        </view>
        <!-- 关闭按钮：仅在 closeable 为 true 时显示 -->
        <template v-if="props.closeable">
          <z-icon
            :name="props.closeIcon"
            :custom-class="[HAPTICS_FEEDBACK]"
            :custom-style="closeIconStyle"
            @click="onClose"
          />
        </template>
      </view>
    </template>

    <!-- ==================== 标签页主体 ==================== -->
    <view :class="bem('tabs')">

      <!-- 标签导航栏：水平可滚动的 tab 标签行 -->
      <view :class="bem('tab-nav')">
        <scroll-view scroll-x :class="bem('tab-nav-scroll')">
          <view :class="bem('tab-nav-inner')">
            <!--
              每个 tab 标签：
              - 已选中 → 显示选项文字（加粗、高亮色）
              - 未选中 → 显示 placeholder 文案（普通字重）
            -->
            <view
              v-for="(tab, tabIndex) in tabs"
              :key="tabIndex"
              :class="[
                bem('tab-item', { active: activeTab === tabIndex })
              ]"
              :style="tabNavStyle(tab)"
              @click="onClickTabItem(tabIndex)"
            >
              {{ tab.selected ? tab.selected[textKey] : (props.placeholder || '请选择') }}
            </view>
          </view>
        </scroll-view>
      </view>

      <!--
        标签内容区：使用 v-if 只渲染当前激活的列。
        每次 activeTab 变化都会重建该列，从而重新触发 CSS 进入动画
        （淡入 + 轻微右移），实现平滑的切换过渡效果。
        纯 CSS 实现，兼容 H5 / App / 小程序等多端。
      -->
      <template v-for="(tab, tabIndex) in tabs" :key="tabIndex">
        <view
          v-if="activeTab === tabIndex"
          :key="activeTab"
          :class="bem('tab-content', 'enter')"
        >
          <!-- 自定义选项上方内容插槽 -->
          <template v-if="instance.slots['options-top']">
            <slot name="options-top" :tab-index="tabIndex"></slot>
          </template>

          <!-- 当前层级选项列表（垂直滚动） -->
          <scroll-view :class="bem('options')" scroll-y="true">
            <template
              v-for="(option, optionIndex) in tab.options"
              :key="optionIndex"
            >
              <!--
                单个选项：
                - selected：选中态（加粗 + 对勾图标）
                - disabled：禁用态（灰色 + 不可点击）
                - className：外部传入的自定义类名
              -->
              <view
                :class="[
                  bem('option', {
                    selected: optionSelected(option, tab.selected),
                    disabled: option.disabled
                  }),
                  option.className
                ]"
                :style="{
                  color: optionColor(
                    option,
                    optionSelected(option, tab.selected)
                  )
                }"
                @click="() => onSelect(option, tabIndex)"
              >
                <!-- 自定义选项内容插槽（可覆盖默认文字） -->
                <template v-if="instance.slots.option">
                  <slot
                    name="option"
                    :option="option"
                    :selected="optionSelected(option, tab.selected)"
                  ></slot>
                </template>
                <template v-else>
                  <text>{{ option[textKey] }}</text>
                </template>

                <!-- 选中态对勾图标 -->
                <template v-if="optionSelected(option, tab.selected)">
                  <z-icon name="check" :custom-style="selectedIconStyle" />
                </template>
              </view>
            </template>
          </scroll-view>

          <!-- 自定义选项下方内容插槽 -->
          <template v-if="instance.slots['options-bottom']">
            <slot name="options-bottom" :tab-index="tabIndex"></slot>
          </template>
        </view>
      </template>
    </view>
  </view>
</template>

<script lang="ts" setup>
import {
  ref,
  watch,
  type PropType,
  getCurrentInstance,
  computed,
  onMounted
} from 'vue'
import {
  extend,
  truthProp,
  numericProp,
  makeArrayProp,
  makeStringProp,
  createNamespace,
  HAPTICS_FEEDBACK,
  type Numeric,
  useComponentName
} from '../../libs/utils'
import zIcon from '../z-icon/z-icon.vue'
import type { CascaderTab, CascaderOption, CascaderFieldNames } from './types'

// ==================== 组件基础 ====================
const [name, bem] = createNamespace('cascader')
useComponentName(name)
const instance = getCurrentInstance()!

// ==================== Props ====================
const props = defineProps({
  title: String,                                      // 顶部标题
  options: makeArrayProp<CascaderOption>(),           // 可选项数据源
  closeable: truthProp,                               // 是否显示关闭图标，默认 true
  swipeable: truthProp,                               // 是否支持手势滑动（保留接口兼容性）
  closeIcon: makeStringProp('close'),                 // 关闭图标名称，默认 'close'
  showHeader: truthProp,                              // 是否展示标题栏，默认 true
  modelValue: numericProp,                            // v-model 选中值
  fieldNames: Object as PropType<CascaderFieldNames>, // 自定义字段名映射
  placeholder: String,                                // 未选中时的提示文案
  activeColor: String                                 // 选中高亮颜色
})

// ==================== Emits ====================
const emit = defineEmits([
  'close',              // 点击关闭图标
  'change',             // 选中项变化时触发 { value, tabIndex, selectedOptions }
  'finish',             // 全部选择完成时触发 { value, tabIndex, selectedOptions }
  'clickTab',           // 点击标签时触发 tabIndex, title
  'update:modelValue'   // v-model 更新
])

// ==================== 响应式状态 ====================

/** 多级标签数据，每个 tab 包含当前层级的所有 options 和已选中的 option */
const tabs = ref<CascaderTab[]>([])

/** 当前激活的标签索引（控制 v-show 切换内容列） */
const activeTab = ref(0)

/** 关闭图标样式（CSS 变量驱动，支持主题定制） */
const closeIconStyle = computed(() => {
  const styles = {
    color: 'var(--z-cascader-close-icon-color)',
    fontSize: 'var(--z-cascader-close-icon-size)'
  }
  return styles
})

// ==================== 字段名映射 ====================

/**
 * 从 props.fieldNames 合并默认字段名
 * 默认：{ text: 'text', value: 'value', children: 'children' }
 * 可通过 field-names 属性自定义，例如 { text: 'name', value: 'code', children: 'items' }
 */
const {
  text: textKey,        // 选项文字字段名
  value: valueKey,      // 选项值字段名
  children: childrenKey // 子选项字段名
} = extend(
  {
    text: 'text',
    value: 'value',
    children: 'children'
  },
  props.fieldNames
)

// ==================== 样式计算 ====================

/**
 * 计算标签栏单个 tab 的样式
 * - 已选中 → 加粗 + 主题色（或 activeColor）
 * - 未选中 → 普通字重 + 灰色
 */
const tabNavStyle = (tab: any) => {
  const styles: any = {
    color: 'var(--z-cascader-tab-color)',
    fontWeight: 'var(--z-font-bold)'
  }
  if (!tab.selected) {
    styles['color'] = 'var(--z-cascader-unselected-tab-color)'
    styles['fontWeight'] = 'normal'
  }
  if (props.activeColor && tab.selected) {
    styles['color'] = props.activeColor
  }
  return styles
}

/** 选中对勾图标样式 */
const selectedIconStyle = computed(() => {
  const styles = {
    fontSize: 'var(--z-cascader-selected-icon-size)'
  }
  return styles
})

// ==================== 选项判断工具 ====================

/**
 * 判断选项是否被选中
 * @param option 当前选项
 * @param selectedOption 该层级已选中的选项
 */
const optionSelected = (option: any, selectedOption: any) => {
  return !!(selectedOption && option[valueKey] === selectedOption[valueKey])
}

/**
 * 获取选项文字颜色
 * 优先级：option.color > 选中态 activeColor > 无（继承默认）
 */
const optionColor = (option: any, selected: any) => {
  return option.color || (selected ? props.activeColor : undefined)
}

// ==================== 数据查找 ====================

/**
 * 根据 value 在树形 options 中递归查找，返回从根到目标节点的完整路径
 * 例如 value='330100' → [{浙江省}, {杭州市}]
 * @returns 路径数组或 undefined（未找到）
 */
const getSelectedOptionsByValue = (
  options: CascaderOption[],
  value: Numeric
): CascaderOption[] | undefined => {
  for (const option of options) {
    // 命中当前层级
    if (option[valueKey] === value) {
      return [option]
    }
    // 递归查找子级
    if (option[childrenKey]) {
      const selectedOptions = getSelectedOptionsByValue(
        option[childrenKey],
        value
      )
      if (selectedOptions) {
        return [option, ...selectedOptions]
      }
    }
  }
}

// ==================== 标签数据构建 ====================

/**
 * 构建 / 重建多级标签数据（核心逻辑）
 *
 * 工作流程：
 * 1. 若 modelValue 有值 → 递归查找选中路径，构建多级 tabs
 * 2. 若 modelValue 无值或未找到 → 回退为单级 tab（根级 options）
 *
 * tabs 结构示例（选中"浙江省 > 杭州市"后）：
 * [
 *   { options: [浙江省, 江苏省], selected: 浙江省 },   // tab 0：省份列
 *   { options: [杭州市, 宁波市], selected: 杭州市 },   // tab 1：城市列
 *   { options: [西湖区, 余杭区], selected: null }      // tab 2：区县列（待选）
 * ]
 */
const updateTabs = () => {
  const { options, modelValue } = props

  // 有预设值时，根据值构建多级 tabs
  if (modelValue !== undefined) {
    // @ts-ignore
    const selectedOptions = getSelectedOptionsByValue(options, modelValue)

    if (selectedOptions) {
      let optionsCursor = options

      // 逐级构建 tab：每级记录当前可选列表 + 已选中项
      // @ts-ignore
      tabs.value = selectedOptions.map((option) => {
        const tab = {
          options: optionsCursor,
          selected: option
        }
        // 找到当前选项在 cursor 中的位置，获取其子级作为下一级 options
        // @ts-ignore
        const next = optionsCursor.find(
          (item) => item[valueKey] === option[valueKey]
        )
        if (next) {
          optionsCursor = next[childrenKey]
        }
        return tab
      })

      // 如果还有下一级数据，追加一个待选的 tab
      if (optionsCursor) {
        tabs.value.push({
          // @ts-ignore
          options: optionsCursor,
          selected: null
        })
      }

      // 激活到最后一个 tab（待选区）
      activeTab.value = tabs.value.length - 1
      return
    }
  }

  // 无预设值或未找到 → 回退为单级 tab
  tabs.value = [
    {
      // @ts-ignore
      options,
      selected: null
    }
  ]
  activeTab.value = 0
}

// ==================== 用户交互 ====================

/**
 * 点击选项
 *
 * 流程：
 * 1. 标记当前 tab 的 selected
 * 2. 截断后续 tab（重新选择）
 * 3. 若有子级 → 追加新 tab 并切换到下一级
 * 4. emit 相关事件
 */
const onSelect = (option: CascaderOption, tabIndex: number) => {
  // 禁用项不可选
  if (option.disabled) {
    return
  }

  // 标记当前层级选中项
  tabs.value[tabIndex].selected = option

  // 如果后面还有 tab（之前选了更深层级），截断它们
  if (tabs.value.length > tabIndex + 1) {
    tabs.value = tabs.value.slice(0, tabIndex + 1)
  }

  // 有子级数据 → 追加下一级 tab
  if (option[childrenKey]) {
    const nextTab = {
      options: option[childrenKey],
      selected: null
    }

    if (tabs.value[tabIndex + 1]) {
      // 替换已有下一级（重新选择场景）
      tabs.value[tabIndex + 1] = nextTab
    } else {
      // 新增下一级
      tabs.value.push(nextTab)
    }

    // 切换到新追加的 tab
    activeTab.value = tabIndex + 1
  }

  // 收集已选中的完整路径（过滤掉 null 的待选区）
  const selectedOptions = tabs.value.map((tab) => tab.selected).filter(Boolean)

  // 同步 v-model
  emit('update:modelValue', option[valueKey])

  // 触发 change 事件
  const params = {
    value: option[valueKey],
    tabIndex,
    selectedOptions
  }
  emit('change', params)

  // 无子级 → 选择完成，触发 finish 事件
  if (!option[childrenKey]) {
    emit('finish', params)
  }
}

/** 点击关闭图标 */
const onClose = () => emit('close')

/**
 * 点击标签栏 tab
 * 切换到对应层级（例如从"区县"切回"省份"重新选择）
 */
const onClickTabItem = (tabIndex: number) => {
  const tab = tabs.value[tabIndex]
  activeTab.value = tabIndex
  emit('clickTab', tabIndex, tab.selected ? tab.selected[textKey] : '')
}

// ==================== 监听器 ====================

/** options 变化时重建 tabs */
watch(() => props.options, updateTabs, { deep: true })

/**
 * modelValue 变化时重建 tabs
 * 优化：若新值已在当前 tabs 的 selected 路径中，跳过重建（避免用户选择时重复触发）
 */
watch(
  () => props.modelValue,
  (value) => {
    if (value !== undefined) {
      // 检查新值是否已在当前选中路径中
      const values = tabs.value.map((tab) => tab.selected?.[valueKey])
      if (values.includes(value)) {
        return // 无需重建
      }
    }
    updateTabs()
  }
)

/** 组件初始化时构建 tabs */
updateTabs()

/**
 * 组件挂载标记
 * 保留此变量兼容外部可能依赖的逻辑
 */
const resizeTabs = ref(true)
onMounted(() => {
  resizeTabs.value = true
})
</script>

<script lang="ts">
/**
 * ZCascader — 级联选择器
 *
 * 用于多层级数据的选择（如省市区），用户逐级点击直到完成所有层级。
 *
 * 本实现完全自包含标签页逻辑（不依赖 z-tabs），通过 v-show 切换内容列，
 * 避免了 z-tabs animated/swipeable 模式下的递归更新问题。
 *
 * @see https://zebraui.com/cascader
 */
export default {
  name: 'ZCascader',
  options: {
    virtualHost: true
  }
}
</script>

<style lang="scss" scoped>
// ==================== 过渡动画关键帧 ====================

// 内容列进入动画：从右侧 40rpx 淡入并归位
@keyframes z-cascader-fade-in {
  from {
    opacity: 0;
    transform: translateX(40rpx);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

// 标签项激活态进入动画（用于标签文字切换时轻微放大提示）
@keyframes z-cascader-tab-pulse {
  0% {
    opacity: 0.5;
    transform: scale(0.94);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

.z-cascader {
  // ==================== 标题栏 ====================
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: var(--z-cascader-header-height);
    padding: var(--z-cascader-header-padding);
  }

  &__title {
    font-size: var(--z-cascader-title-font-size);
    font-weight: var(--z-font-bold);
    line-height: var(--z-cascader-title-line-height);
    color: var(--z-text-color);
  }

  // ==================== 标签区域外层容器 ====================
  &__tabs {
    padding: 0 var(--z-padding-xs);
  }

  // ==================== 标签导航栏 ====================
  &__tab-nav {
    height: var(--z-cascader-tabs-height, 96rpx);
    overflow: hidden;
  }

  // 水平滚动容器
  &__tab-nav-scroll {
    width: 100%;
    height: 100%;
    white-space: nowrap;
  }

  // 标签项弹性布局
  &__tab-nav-inner {
    display: flex;
    align-items: center;
    height: 100%;
    column-gap: 16rpx;
    transition: all 0.4s ease;
  }

  // 单个标签项
  &__tab-item {
    flex-shrink: 0;
    padding: 0 var(--z-padding-sm);
    font-size: var(--z-font-size-md);
    line-height: var(--z-cascader-tabs-height, 96rpx);
    cursor: pointer;
    user-select: none;
    border-radius: 12px;
    box-shadow: var(--aye-shadow-inset);
    transition: all 0.4s ease;

    // 激活态高亮：颜色由 JS（tabNavStyle）动态控制，
    // 此处补充轻微的放大/淡入动画增强切换反馈
    &--active {
      animation: z-cascader-tab-pulse 0.3s ease;
    }
  }

  // 当前激活的 tab 内容容器（v-if 渲染），带进入过渡动画
  // 当 activeTab 变化时重新挂载，触发 fade-in 动画（淡入 + 轻微右移）
  &__tab-content {
    &--enter {
      animation: z-cascader-fade-in 0.35s ease both;
    }
  }

  // ==================== 选项列表 ====================
  &__option {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20rpx var(--z-padding-xs);
    font-size: var(--z-font-size-md);
    line-height: var(--z-line-height-md);
    color: var(--z-text-color);
    cursor: pointer;
    // 选项选中/点击状态的颜色、背景、字体平滑过渡
    transition:
      color 0.25s ease,
      background-color 0.25s ease,
      font-weight 0.25s ease;

    // 点击态反馈
    &:active {
      background-color: var(--z-active-color);
    }

    // 选中态
    &--selected {
      font-weight: var(--z-font-bold);
      color: var(--z-cascader-active-color);
    }

    // 禁用态
    &--disabled {
      color: var(--z-cascader-option-disabled-color);
      cursor: not-allowed;

      &:active {
        background-color: transparent;
      }
    }
  }

  // 选项滚动区域
  &__options {
    box-sizing: border-box;
    height: var(--z-cascader-options-height);
    padding-top: 12rpx;
  }
}
</style>
