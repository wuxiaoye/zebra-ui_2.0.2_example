<template>
  <!-- 复选框组外层容器，区分横竖布局 -->
  <view class="aye-checkbox-group" :class="{ 'group-vertical': layout === 'vertical' }">
    <!-- 插槽承载所有子复选框 -->
    <slot />
  </view>
</template>

<script setup>
import { provide, computed, toRefs, reactive } from 'vue'

/**
 * 组组件入参
 */
const props = defineProps({
  // v-model绑定选中值数组
  modelValue: {
    type: Array,
    default: () => []
  },
  // 最大可选数量，兼容字符串数字 max="3"
  max: {
    type: [Number, String],
    default: 999,
    validator(val) {
      const num = Number(val)
      return !isNaN(num) && num >= 0
    }
  },
  layout: {
    type: String,
    default: 'horizontal',
    validator: val => ['horizontal', 'vertical'].includes(val)
  },
  // 向下全局透传给子项的样式参数
  shape: String,
  disabled: Boolean,
  activeIconColor: String,
  inactiveIconColor: String,
  labelColor: String,
  labelSize: String,
  iconSize: String,
  verticalFull: Boolean,
  reverseVerticalFull: Boolean
})

/**
 * 对外抛出事件
 * update:modelValue 用于v-model
 * change 组整体选中变化事件，参数为最新选中数组
 */
const emit = defineEmits(['update:modelValue', 'change'])

// 存储所有子项状态：Map<value, 是否禁用>
const optionStatusMap = reactive(new Map())

// 注册子项value与禁用状态
const registerOption = (val, isDisabled) => {
  optionStatusMap.set(val, isDisabled)
}
// 卸载子项
const unregisterOption = (val) => {
  optionStatusMap.delete(val)
}

// 计算属性：过滤掉禁用项，得到可操作有效值数组
const availableOptions = computed(() => {
  const list = []
  optionStatusMap.forEach((disabled, val) => {
    if (!disabled) list.push(val)
  })
  return list
})

// 劫持v-model，赋值时同时触发change事件
const innerValue = computed({
  get() {
    return props.modelValue
  },
  set(newVal) {
    emit('update:modelValue', newVal)
    // 组触发change事件，传出最新选中列表
    emit('change', newVal)
  }
})

// 转为纯数字最大选择数
const realMax = computed(() => Number(props.max))

/**
 * 单个子项点击切换
 * @param {*} val 当前点击的value
 */
const handleItemChange = (val) => {
  const arr = [...innerValue.value]
  const idx = arr.indexOf(val)
  const maxNum = realMax.value

  if (idx > -1) {
    arr.splice(idx, 1)
  } else {
    if (arr.length >= maxNum) {
      uni.showToast({ title: `最多选择${maxNum}项`, icon: 'none', duration: 1500 })
      return
    }
    arr.push(val)
  }
  innerValue.value = arr
}

/**
 * 全选：只勾选非禁用项，受max限制
 * @param {Array} allValues 外部传入全部数据源（兼容旧调用）
 */
const selectAll = (allValues = []) => {
  const validList = availableOptions.value.length
    ? availableOptions.value
    : allValues.filter(item => !optionStatusMap.get(item))

  innerValue.value = validList.slice(0, realMax.value)
}

/**
 * 反选：仅在可用非禁用项内取反，禁用项不参与
 * @param {Array} allValues 外部全部数据源
 */
const invertSelect = (allValues = []) => {
  const validList = availableOptions.value.length
    ? availableOptions.value
    : allValues.filter(item => !optionStatusMap.get(item))

  const selectedValid = innerValue.value.filter(v => validList.includes(v))
  const invertList = validList.filter(item => !selectedValid.includes(item))

  innerValue.value = invertList.slice(0, realMax.value)
}

/**
 * 清空所有选中
 */
const clearAll = () => {
  innerValue.value = []
}

// 注入给子组件的全部能力
provide('ayeCheckboxGroup', {
  innerValue,
  handleItemChange,
  groupGlobalProps: toRefs(props),
  registerOption,
  unregisterOption,
  selectAll,
  invertSelect,
  clearAll
})

// 暴露实例方法给ref调用
defineExpose({
  selectAll,
  invertSelect,
  clearAll
})
</script>

<style scoped>
/* 默认横向自动换行 */
.aye-checkbox-group {
  display: flex;
  flex-wrap: wrap;
  gap: 24rpx;
}
/* 竖向单列排列 */
.aye-checkbox-group.group-vertical {
  flex-direction: column;
}
</style>