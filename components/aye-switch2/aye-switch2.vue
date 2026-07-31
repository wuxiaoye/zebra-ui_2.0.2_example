<template>
  <!-- <view class="aye-switch" :style="switchStyle" @tap="toggle">
    <view class="aye-switch-track" :class="{ checked: modelValue }"></view>
    <view class="aye-switch-thumb" :class="{ checked: modelValue }"></view>
  </view> -->
  
  <view class="neu-toggle-track" :style="switchStyle"  :class="{ active: modelValue }" @tap="toggle">
    <view class="neu-toggle-thumb"></view>
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
  const heightNum = num * 0.54;
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


.neu-toggle-track {
  width: 88rpx;
  height: 48rpx;
  background: var(--greyLight-1);
  box-shadow: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
  border-radius: 24rpx;
  position: relative;
  cursor: pointer;
  transition: background 0.4s ease;
   /* 宽高由 CSS 自定义属性控制 */
    width: var(--sw-width);
    height: var(--sw-height);
    border-radius: calc(var(--sw-height) / 2);
}

.neu-toggle-thumb {
  width: 36rpx;
  height: 36rpx;
  background: var(--greyLight-2);
  box-shadow: 0.2rem 0.2rem 0.4rem var(--greyLight-2), -0.15rem -0.15rem 0.3rem var(--white);
  border-radius: 50%;
  position: absolute;
  top: 6rpx;
  left: 6rpx;
  transition: all 0.4s ease;
  /* 圆点尺寸为宽度的 35%，保持正方形 */
    width: calc(var(--sw-width) * 0.4);
    height: calc(var(--sw-width) * 0.4);
    /* 未选中时 left = 宽度 * 6/88 */
    left: calc(var(--sw-width) * 0.068);
    /*  top = 高度 * 0.125 */
    top: calc(var(--sw-height) * 0.125);
}

.neu-toggle-track.active {
  background: var(--primary-light);
}

.neu-toggle-track.active .neu-toggle-thumb {
  left: 46rpx;
  background: var(--white);
  /* 选中时 left = 宽度 * 46/88 */
  left: calc(var(--sw-width) * 0.522);
}


</style>