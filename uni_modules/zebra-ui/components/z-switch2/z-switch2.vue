<!-- components/AyeSwitch/index.vue -->
<template>
  <view class="aye-switch" 
         :class="{ 'is-disabled': disabled }"
        :style="switchStyle" 
        @tap="toggle"
    >
    <view class="aye-switch-track" :class="{ checked: modelValue }"></view>
    <view class="aye-switch-thumb" :class="{ checked: modelValue }"></view>
  </view>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  /** 开关宽度，支持任意 CSS 长度单位（如 '120rpx', '100px', '10vw'） */
  width: {
    type: String,
    default: '90rpx'
  },
  modelValue: {
    type: Boolean,
    default: false
  },
  /** 是否禁用 */
  disabled: {
    type: Boolean,
    default: false
  },
  /** 是否启用异步控制：为 true 时，点击不自动更新 modelValue，仅触发 change 事件由父组件异步控制 */
  asyncChange: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['update:modelValue', 'change']);

// 解析宽度，生成 CSS 自定义属性
const switchStyle = computed(() => {
  const match = props.width.match(/^([\d.]+)(.*)$/);
  let num = 120, unit = 'rpx';
  if (match) {
    num = parseFloat(match[1]);
    unit = match[2] || 'rpx';
  }
  const heightNum = num / 2;
  return {
    '--sw-width': num + unit,
    '--sw-height': heightNum + unit
  };
});

const toggle = () => {
  if (props.disabled) {
    uni.showToast({ title: '已禁用', icon: 'none' });
    return;
  }

  const newVal = !props.modelValue;

  // 如果是异步控制模式，不更新 modelValue，只触发 change 事件
  if (props.asyncChange) {
    emit('change', newVal);
  } else {
    // 普通模式：更新 v-model 并触发 change
    emit('update:modelValue', newVal);
    emit('change', newVal);
  }
};
</script>

<style scoped>

.aye-switch {
  display: flex;
  align-items: center;
  position: relative;
  width: var(--sw-width);
  height: var(--sw-height);
  border-radius: calc(var(--sw-height) / 2);
  box-shadow: var(--z-switch2-track-shadow);
  background: rgba(255, 255, 255, 0);
  transition: all 0.4s ease;
  cursor: pointer;
}

.aye-switch-track {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: inherit;
  background: var(--z-switch2-track-active-background-color);
  opacity: 0;
  transition: opacity 0.4s ease;
}
.aye-switch-track.checked {
  opacity: 1;
}

.aye-switch-thumb {
  position: absolute;
  width: calc(var(--sw-width) * 0.35);
  height: calc(var(--sw-width) * 0.35);
  border-radius: 50%;
  background: var(--z-switch2-dot-background-color);
  left: calc(var(--sw-width) * 0.0667);
  transition: all 0.4s ease;
}
.aye-switch-thumb.checked {
  left: calc(var(--sw-width) - var(--sw-width) * 0.35 - var(--sw-width) * 0.0667);
  background: var(--z-switch2-dot-active-background-color);
}

.aye-switch.is-disabled {
  cursor: not-allowed;
  opacity: var(--z-switch-disabled-opacity);
}
</style>