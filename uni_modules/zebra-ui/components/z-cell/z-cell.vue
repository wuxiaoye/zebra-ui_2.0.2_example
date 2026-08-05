<template>
  <!--
    z-cell 单元格组件
    prop:
      cellOverflowHidden: boolean = true  根容器是否开启 overflow:hidden；false=允许子元素溢出cell盒子
      valueOverflowHidden: boolean = true value区域是否开启 overflow:hidden；false=value内容可以溢出
    注意：当 required 生效时，根容器强制 overflow:visible，cellOverflowHidden 将失效，保证*必填星号正常显示
  -->
  <view
    :class="[
      bem({
        center,
        required: !!required,
        clickable,
        borderless: !border,
        [size]: !!size,
        // BEM修饰符：cellOverflowHidden为true时增加 z-cell--overflow-hidden
        'overflow-hidden': cellOverflowHidden
      }),
      customClass
    ]"
    :style="customStyle"
    :tabindex="clickable ? 0 : undefined"
    @click="onClick"
  >
    <!-- icon插槽 -->
    <template v-if="showSlots('icon')">
      <slot name="icon"></slot>
    </template>
    <template v-else-if="props.icon">
      <view :class="bem('left-icon')">
        <z-icon :name="props.icon" :class-prefix="props.iconPrefix" :color="props.iconColor" />
      </view>
    </template>

    <!-- title + label 区域 -->
    <template v-if="showSlots('title') || isDef(props.title)">
      <view :class="[bem('title'), props.titleClass]" :style="props.titleStyle">
        <template v-if="showSlots('title')">
          <slot name="title"></slot>
        </template>
        <template v-else>
          {{ props.title }}
        </template>

        <!-- label副标题 -->
        <template v-if="showSlots('label') || isDef(props.label)">
          <view :class="[bem('label'), props.labelClass]">
            <template v-if="showSlots('label')">
              <slot name="label"></slot>
            </template>
            <template v-else>
              {{ props.label }}
            </template>
          </view>
        </template>
      </view>
    </template>

    <!-- value区域：默认插槽 / value插槽 / value属性 -->
    <template v-if="showSlots('default') || showSlots('value') || isDef(props.value)">
      <!--
        bem第二个参数对象，valueOverflowHidden=true，生成类名 z-cell__value--overflow-hidden
        valueOverflowHidden=false，则不添加该修饰类，overflow为visible
      -->
      <view
        :class="[bem('value', { 'overflow-hidden': valueOverflowHidden }), props.valueClass]"
        :style="props.valueStyle"
      >
        <!-- default插槽优先，兼容老代码，default映射value展示区 -->
        <template v-if="showSlots('default')">
          <slot></slot>
        </template>
        <template v-else-if="showSlots('value')">
          <slot name="value"></slot>
        </template>
        <template v-else>
          {{ props.value }}
        </template>
      </view>
    </template>

    <!-- 右侧图标插槽 / link箭头 -->
    <template v-if="showSlots('right-icon')">
      <slot name="right-icon"></slot>
    </template>
    <template v-else-if="props.isLink">
      <view :class="bem('right-icon')">
        <z-icon
          :custom-style="rightIconStyle"
          :name="
            props.arrowDirection && props.arrowDirection !== 'right'
              ? `${props.arrowDirection}-big`
              : 'right-big'
          "
        />
      </view>
    </template>

    <!-- extra扩展插槽 -->
    <slot name="extra"></slot>
  </view>
</template>

<script lang="ts" setup>
import { type PropType, getCurrentInstance, computed } from 'vue'
import {
  isDef,
  truthProp,
  unknownProp,
  numericProp,
  createNamespace,
  isObject,
  useComponentName
} from '../../libs/utils'
import zIcon from '../z-icon/z-icon.vue'

const emit = defineEmits(['click'])
const instance = getCurrentInstance()
const [name, bem] = createNamespace('cell')
useComponentName(name)

type CellSize = 'normal' | 'large'
type CellArrowDirection = 'up' | 'down' | 'left' | 'right'

const props = defineProps({
  icon: String,
  iconColor: String,
  size: String as PropType<CellSize | any>,
  title: numericProp,
  value: numericProp,
  label: numericProp,
  center: Boolean,
  isLink: Boolean,
  border: truthProp,
  iconPrefix: String,
  valueClass: unknownProp,
  valueStyle: null as unknown as PropType<string | any>,
  labelClass: unknownProp,
  titleClass: unknownProp,
  titleStyle: null as unknown as PropType<string | any>,
  arrowDirection: String as PropType<CellArrowDirection>,
  required: {
    type: [Boolean, String] as PropType<boolean | 'auto'>,
    default: null
  },
  clickable: {
    type: Boolean as PropType<boolean | null>,
    default: null
  },
  customStyle: Object,
  customClass: [String, Object],
  rightIconStyle: Object,
  componentSlots: Object,

  /**
   * 根容器是否开启 overflow:hidden
   * @default true
   * @description 设置false，允许子元素溢出cell盒子，常用于气泡、下拉组件；注意：分割线hairline可能会溢出
   */
  cellOverflowHidden: {
    type: Boolean,
    default: true
  },
  /**
   * value区域是否开启 overflow:hidden
   * @default true
   * @description 设置false，value插槽内的内容可以向外溢出；min‑width:0保证flex布局不会被长内容挤乱
   */
  valueOverflowHidden: {
    type: Boolean,
    default: true
  }
})

// 可点击判断：isLink也代表可点击
const clickable: any = props.clickable ? props.clickable : props.isLink

const onClick = () => {
  emit('click')
}

/**
 * 兼容组件传slot对象模式，uni‑app部分场景需要组件内判断插槽是否传入
 */
const componentSlotsShow = computed(() => {
  return isObject(props.componentSlots)
})

/**
 * 判断指定插槽是否存在
 * @param name 插槽名
 */
const showSlots = (name: string) => {
  if (componentSlotsShow.value) {
    if (name == 'default') {
      return props.componentSlots!['value'] ? props.componentSlots!['value'] : false
    }
    return props.componentSlots![name] ? props.componentSlots![name] : false
  }
  return instance!.slots[name]
}
</script>

<script lang="ts">
export default {
  name: 'ZCell',
  options: {
    virtualHost: true
  }
}
</script>

<style lang="scss" scoped>
@import '../z-style/mixins/hairline';

.z-cell {
  position: relative;
  box-sizing: border-box;
  display: flex;
  width: 100%;
  padding: var(--z-cell-vertical-padding) var(--z-cell-horizontal-padding);
  /* ❗删除写死overflow:hidden，交给修饰符 &--overflow-hidden控制 */
  font-size: var(--z-cell-font-size);
  line-height: var(--z-cell-line-height);
  color: var(--z-cell-text-color);
  background: var(--z-cell-background);

  /**
   * BEM修饰符 z-cell--overflow-hidden
   * prop cellOverflowHidden = true 才会加上这个类，开启超出隐藏
   */
  &--overflow-hidden {
    overflow: hidden;
  }

  // hairline 底部分割线伪元素，transform实现1px细线
  &::before {
    @include hairline-bottom(
      var(--z-cell-border-color),
      var(--z-padding-md),
      var(--z-padding-md)
    );
  }

  // 最后一项和无边框模式，隐藏分割线
  &:last-child::before,
  &--borderless::before {
    display: none;
  }

  /**
   * 必填项，显示*号，优先级最高，强制overflow:visible
   * 即使 cellOverflowHidden=true，这里也要覆盖，否则*号会被裁切看不见
   */
  &--required {
    overflow: visible !important;
    &::before {
      position: absolute;
      left: var(--z-padding-xs);
      font-size: var(--z-cell-font-size);
      color: var(--z-cell-required-color);
      content: '*';
    }
  }

  &__label {
    margin-top: var(--z-cell-label-margin-top);
    font-size: var(--z-cell-label-font-size);
    line-height: var(--z-cell-label-line-height);
    color: var(--z-cell-label-color);
  }

  &__title,
  &__value {
    flex: 1;
  }

  &__value {
    position: relative;
    /**
     * ✅关键：min‑width:0，强制开启flex收缩，不再依赖overflow:hidden
     * 无论 value‑overflow‑hidden true/false，长内容都不会把title挤没
     */
    min-width: 0;
    font-size: var(--z-cell-value-font-size);
    color: var(--z-cell-value-color);
    text-align: right;
    word-wrap: break-word;
    vertical-align: middle;
    /* ❗删除写死overflow:hidden，交给修饰符控制 */

    /**
     * BEM修饰符 z-cell__value--overflow-hidden
     * prop valueOverflowHidden = true，开启value区域超出隐藏
     */
    &--overflow-hidden {
      overflow: hidden;
    }
  }

  &__left-icon,
  &__right-icon {
    height: var(--z-cell-line-height);
    font-size: var(--z-cell-icon-size);
    line-height: var(--z-cell-line-height);
  }

  &__left-icon {
    margin-right: var(--z-padding-base);
  }

  &__right-icon {
    margin-left: var(--z-padding-base);
    color: var(--z-cell-right-icon-color);
  }

  &--clickable {
    cursor: pointer;
    &:active {
      background-color: var(--z-cell-active-color);
    }
  }

  &--center {
    align-items: center;
  }

  &--large {
    padding-top: var(--z-cell-large-vertical-padding);
    padding-bottom: var(--z-cell-large-vertical-padding);
    .z-cell__title {
      font-size: var(--z-cell-large-title-font-size);
    }
    .z-cell__label {
      font-size: var(--z-cell-large-label-font-size);
    }
    .z-cell__value {
      font-size: var(--z-cell-large-value-font-size);
    }
  }
}
</style>