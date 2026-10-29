<template>
  <input
    class="form__input"
    :placeholder="placeholder"
    :value="modelValue"
    @input="onInput"
    placeholder-class="form-placeholder"
    :placeholder-style="placeholderStyle"
  />
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  modelValue: { type: String, default: '' },
  placeholder: { type: String, default: '请输入文字...' },
  /** placeholder 颜色，支持任意 CSS 颜色值 */
  placeholderColor: { type: String, default: '#bec8e4' }
});

const emit = defineEmits(['update:modelValue']);

const onInput = (e) => {
  emit('update:modelValue', e.detail.value);
};

// 生成内联样式字符串，也可直接绑定对象
const placeholderStyle = computed(() => `color: ${props.placeholderColor};`);
</script>

<style scoped>
/* 使用深度选择器确保 placeholder-class 样式也能生效（备用） */
::v-deep .form-placeholder {
  color: v-bind(placeholderColor); /* 如果支持 v-bind in CSS，可直接绑定，但为了兼容性保留内联 */
  /* 其他样式如 font-size, font-weight 等可在此定义 */
}

.form__input {
  width: 100%;
  height: 80rpx;
  border: none;
  border-radius: 20rpx;
  font-size: 28rpx;
  padding-left: 28rpx;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
  background: none;
  color: var(--greyDark);
}
</style>