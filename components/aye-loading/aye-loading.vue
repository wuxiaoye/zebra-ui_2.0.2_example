<template>
  <view
    class="neu-card loading-card"
    :style="{
      flexDirection: props.isVertical ? 'column' : 'row'
    }"
  >
    <view
      class="spinner-wrap"
      :style="{
        width: props.size,
        height: props.size,
        margin: props.isVertical ? '0 0 24rpx 0' : '0 24rpx 0 0'
      }"
    >
      <view class="neu-spinner" :style="spinnerStyle"></view>
    </view>
    <text
      class="forum-caption"
      v-if="props.isShowText"
      :style="textStyle"
    >
      <slot>加载中...</slot>
    </text>
  </view>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  isVertical: {
    type: Boolean,
    default: false
  },
  // 图标大小，带单位
  size: {
    type: String,
    default: '72rpx'
  },
  isShowText: {
    type: Boolean,
    default: true
  },
  textSize: {
    type: String,
    default: '24rpx'
  },
  textColor: {
    type: String,
    default: 'var(--greyDark)'
  },
  // 【新增】支持自定义线条颜色
  color: {
    type: String,
    default: 'var(--primary)'
  },
  // 【新增】线条粗细
  borderWidth: {
    type: String,
    default: '6rpx'
  }
});

const textStyle = computed(() => {
  return {
    fontSize: props.textSize,
    color: props.textColor
  };
});

// 动态样式绑定圆环颜色、线条宽度
const spinnerStyle = computed(() => ({
  borderWidth: props.borderWidth,
  borderTopColor: props.color,
  borderLeftColor: props.color
}))
</script>

<style scoped>
@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.loading-card {
  display: flex;
  justify-content: center;
  align-items: center;
}

.spinner-wrap {
  border-radius: 50%;
  box-shadow: var(--aye-shadow);
}

.neu-spinner {
  width: 100%;
  height: 100%;
  border-style: solid;
  border-color: var(--greyLight-2);
  border-right-color: transparent;
  border-bottom-color: transparent;
  border-radius: 50%;
  box-sizing: border-box;
  animation: spin 1s linear infinite;
}

.forum-caption {
  font-size: 24rpx;
  color: var(--greyDark);
  line-height: 1.5;
}
</style>