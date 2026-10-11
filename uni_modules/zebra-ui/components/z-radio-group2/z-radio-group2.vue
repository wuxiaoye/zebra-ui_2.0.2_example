<template>
  <view class="aye-radio-group" :class="[layout === 'vertical' ? 'vertical-group' : '']">
    <slot />
  </view>
</template>

<script setup>
import { provide, computed, toRefs } from 'vue'

const props = defineProps({
  modelValue: {
    type: [String, Number],
    default: ''
  },
  layout: {
    type: String,
    default: 'horizontal',
    validator: v => ['horizontal', 'vertical'].includes(v)
  },
  disabled: {
    type: Boolean,
    default: false
  },
  iconSize: {
    type: String,
    default: undefined
  },
  iconActiveColor: {
    type: String,
    default: undefined
  },
  iconNormalColor: {
    type: String,
    default: undefined
  },
  labelColor: {
    type: String,
    default: undefined
  },
  labelSize: {
    type: String,
    default: ''
  },
  verticalFull: {
    type: Boolean,
    default: false
  },
  reverseAlign: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['update:modelValue', 'change'])

const currentValue = computed({
  get() {
    return props.modelValue
  },
  set(val) {
    emit('update:modelValue', val)
    emit('change', val)
  }
})

provide('zRadioGroup2', {
  currentValue,
  setCurrent: (val) => {
    currentValue.value = val
  },
  groupProps: toRefs(props)
})
</script>

<style scoped>
.aye-radio-group {
  display: flex;
  flex-wrap: wrap;
  gap: 24rpx;
}
.vertical-group {
  flex-direction: column;
}
</style>