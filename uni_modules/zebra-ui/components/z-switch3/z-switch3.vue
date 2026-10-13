<template>
  <view class="neu-toggle-track" 
        :style="switchStyle"  
        :class="{ active: modelValue, 'is-disabled': disabled }" 
        @tap="toggle"
    >
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
  },
  /** 新增：是否禁用 */
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
    if (props.disabled){
        uni.showToast({ title: '已禁用', icon:'none' });
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

.neu-toggle-track {
  width: 88rpx;
  height: 48rpx;
  background: var(--z-switch3-track-background-color);
  box-shadow: var(--z-switch3-track-shadow);
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
  background: var(--z-switch3-dot-background-color);
  box-shadow: var(--z-switch3-dot-shadow);
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
  background: var(--z-switch3-track-active-background-color);
}

.neu-toggle-track.active .neu-toggle-thumb {
  left: 46rpx;
  background: var(--z-switch3-dot-active-background-color);
  /* 选中时 left = 宽度 * 46/88 */
  left: calc(var(--sw-width) * 0.522);
}

.neu-toggle-track.is-disabled {
    cursor: not-allowed;
    opacity: var(--z-switch-disabled-opacity);
}
</style>