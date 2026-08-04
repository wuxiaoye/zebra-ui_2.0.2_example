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
  borderRightColor: props.color,
}))
</script>

<style scoped>
:root{
    /* 变量定义 */
    --primary-light: #2fe25f;
    --primary: #07c160;
    --primary-dark: #0eb805;
    --secondary-light: #8abdff;
    --secondary: #6d5dfc;
    --secondary-dark: #5b0eeb;
    --white: #FFFFFF;
    --greyLight-1: #E4EBF5;
    --greyLight-1-dark: #d8e4f5;
    --greyLight-2: #c8d0e7;
    --greyLight-3: #bec8e4;
    --greyDark: #9baacf;
    /* 卡片外阴影样式 -超大*/
    --aye-shadow-more-big: 0.4rem 0.4rem 0.8rem var(--greyLight-2),  -0.4rem -0.4rem 0.8rem var(--white);
    /* 卡片外阴影样式 -大一些*/
    --aye-shadow-big: 6px 6px 12px var(--greyLight-2), -4px -4px 10px var(--white);
     /* 卡片外阴影样式 */
    --aye-shadow:  3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
     /* 卡片外阴影样式 - 小一些*/
    --aye-shadow-mini: 2px 2px 4px var(--greyLight-2), -1px -1px 3px var(--white);
     
     /* 内凹阴影-大一些 */
     --aye-shadow-inset-more-big: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
     /* 内凹阴影 */
    --aye-shadow-inset: inset 2px 2px 4px var(--greyLight-2), inset -2px -2px 4px var(--white);
     /* 内凹阴影-小一些 */
    --aye-shadow-inset-mini: inset 1px 1px 1px var(--greyLight-2), inset -2px -2px 4px var(--white);
}

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
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  border-style: solid;
  border-color: transparent;
   /* var(--greyLight-2) transparent transparent; */
  border-radius: 50%;
  box-shadow: var(--aye-shadow-inset);
  box-shadow: inset -4px -4px 8px var(--white), inset 4px 4px 8px var(--white);
  background: var(--greyLight-1);
  animation: spin 1s linear infinite;
}

.forum-caption {
  font-size: 24rpx;
  color: var(--greyDark);
  line-height: 1.5;
}
</style>