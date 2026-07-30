<!-- components/AyeSwitch/index.vue -->
<template>
  <view class="aye-switch" :style="switchStyle" @tap="toggle">
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
  }
});

const emit = defineEmits(['update:modelValue']);

// 解析宽度，生成 CSS 自定义属性，用于内部样式计算
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
  emit('update:modelValue', !props.modelValue);
};
</script>

<style scoped>
/* 定义全局变量（可迁移至公共样式，这里保留以便独立使用） */
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
  --primary-light: #2fe25f;
  --primary: #07c160;
  --primary-dark: #0eb805;
}

.aye-switch {
  display: flex;
  align-items: center;
  position: relative;
  /* 宽高由 CSS 自定义属性控制 */
  width: var(--sw-width);
  height: var(--sw-height);
  border-radius: calc(var(--sw-height) / 2);
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  background: rgba(255, 255, 255, 0);
  transition: all 0.4s ease;
  cursor: pointer;
}

/* 背景轨道（激活颜色渐变） */
.aye-switch-track {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: inherit;
  background: linear-gradient(330deg, var(--primary-dark) 0%, var(--primary) 50%, var(--primary-light) 100%);
  opacity: 0;
  transition: opacity 0.4s ease;
}
.aye-switch-track.checked {
  opacity: 1;
}

/* 滑块圆点 */
.aye-switch-thumb {
  position: absolute;
  /* 圆点尺寸为宽度的 35%，保持正方形 */
  width: calc(var(--sw-width) * 0.35);
  height: calc(var(--sw-width) * 0.35);
  border-radius: 50%;
  background: var(--greyDark);
  /* 未选中时 left = 宽度 * 8/120 ≈ 宽度 * 0.0667 */
  left: calc(var(--sw-width) * 0.0667);
  transition: all 0.4s ease;
}
.aye-switch-thumb.checked {
  /* 选中时 left = 宽度 - 圆点宽度 - 左边距 */
  left: calc(var(--sw-width) - var(--sw-width) * 0.35 - var(--sw-width) * 0.0667);
  background: var(--greyLight-1);
}
</style>