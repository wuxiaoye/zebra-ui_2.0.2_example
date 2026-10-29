<template>
  <view class="icon-btn" :class="{ pressed: isPressed }" @touchstart="press" @touchend="release" @tap="$emit('click')">
    <!-- 具名插槽 icon，无插槽内容时可保留默认uv-icon兜底 -->
    <slot name="icon">
      <uv-icon :name="icon" :color="isPressed ? '#07c160' : '#9baacf'" size="20" />
    </slot>
  </view>
</template>

<script setup>
import { ref } from 'vue';
// 保留icon props作为插槽兜底默认图标，不传插槽时仍可使用 icon 属性
const props = defineProps({
  icon: {
    type: String,
    default: 'home-fill'
  }
});
const emit = defineEmits(['click']);
const isPressed = ref(false);
const press = () => isPressed.value = true;
const release = () => isPressed.value = false;
</script>

<style scoped>
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
}
.icon-btn {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.2s ease;
}
.icon-btn.pressed {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}
</style>