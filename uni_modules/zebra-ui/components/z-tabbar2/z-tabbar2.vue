<!-- components/AyeSegmentedControl/index.vue -->
<template>
  <view class="segmented-control" :style="controlStyle">
    <!-- Tab 选项 -->
    <view
      v-for="(item, idx) in tabs"
      :key="idx"
      class="segmented-control-item"
      :class="{ active: modelValue === idx }"
      :style="itemStyle"
      @tap="select(idx)"
    >
      <text :style="textStyle">{{ item }}</text>
    </view>

    <!-- 高亮滑块 -->
    <view
      class="segmented-control-inset-box"
      :style="sliderStyle"
    ></view>
  </view>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  /** 当前选中 Tab 索引 */
  modelValue: {
    type: Number,
    default: 0
  },
  /** Tab 数据数组（字符串） */
  tabs: {
    type: Array,
    default: () => ['Tab 1', 'Tab 2', 'Tab 3']
  },
  /** 组件总高度，支持任意 CSS 长度单位（如 '80rpx', '60px', '10vw'） */
  height: {
    type: String,
    default: '80rpx'
  }
});

const emit = defineEmits(['update:modelValue']);

// 解析高度，生成 CSS 变量
const controlStyle = computed(() => {
  const match = props.height.match(/^([\d.]+)(.*)$/);
  let num = 80,
    unit = 'rpx';
  if (match) {
    num = parseFloat(match[1]);
    unit = match[2] || 'rpx';
  }
  return {
    '--seg-height': num + unit,
    '--seg-unit': unit,       // 方便内部计算
    '--seg-num': num          // 数值，用于比例计算
  };
});

// 计算内部尺寸（基于高度比例）
const itemStyle = computed(() => {
  // 假设高度为 H，Tab 项高度为 H - 8rpx（上下各留 4rpx）
  // 滑块高度为 H - 12rpx（上下各留 6rpx）
  // 文字大小约为 H * 0.35
  const h = parseFloat(controlStyle.value['--seg-num']) || 80;
  const unit = controlStyle.value['--seg-unit'] || 'rpx';
  return {
    height: `calc(var(--seg-height) - 8${unit})`,
    lineHeight: `calc(var(--seg-height) - 8${unit})`, // 垂直居中
    fontSize: `calc(var(--seg-height) * 0.35)`,
    // 圆角随高度变化，约为 0.2 * H
    borderRadius: `calc(var(--seg-height) * 0.25)`
  };
});

const textStyle = computed(() => ({
  fontSize: `calc(var(--seg-height) * 0.35)`
}));

// 高亮滑块样式：宽度 = (100% / tabs.length) - 左右边距(6rpx 两侧)，left 动态偏移
const sliderStyle = computed(() => {
  const len = props.tabs.length;
  const unit = controlStyle.value['--seg-unit'] || 'rpx';
  // 左右边距固定为 6rpx，可根据需要调整，这里也随高度缩放？我们保持固定 6rpx，或按比例：
  const margin = `calc(var(--seg-height) * 0.075)`; // 6/80 ≈ 0.075
  const width = `calc(${100 / len}% - ${margin} * 2)`;
  const left = `calc(${props.modelValue * (100 / len)}% + ${margin})`;
  // 滑块高度
  const sliderHeight = `calc(var(--seg-height) - 12${unit})`;
  return {
    height: sliderHeight,
    width: width,
    left: left,
    borderRadius: `calc(var(--seg-height) * 0.2)`
  };
});

const select = (index) => {
  if (index >= 0 && index < props.tabs.length) {
    emit('update:modelValue', index);
  }
};
</script>

<style scoped>
/* CSS 变量（可移至全局） */
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
  --primary: #07c160;
}

.segmented-control {
  width: 100%;
  height: var(--seg-height);
  /* box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white); */
  box-shadow: var(--z-tabbar2-shadow);
  border-radius: calc(var(--seg-height) * 0.25);
  display: flex;
  align-items: center;
  position: relative;
  background: transparent;
  /* 如果高度变化，阴影可能显得不协调，但阴影大小固定为 rpx，可优化但不影响功能 */
}

.segmented-control-item {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  color: var(--greyDark);
  transition: color 0.3s ease;
  position: relative;
  z-index: 10;
  text-align: center;
  /* 高度、字体、行高由内联样式覆盖 */
}

.segmented-control-item.active {
  color: var(--primary);
}

/* 高亮滑块 */
.segmented-control-inset-box {
  position: absolute;
  border-radius: calc(var(--seg-height) * 0.2);
  /* box-shadow: inset 4rpx 4rpx 10rpx #c8d0e7, inset -4rpx -4rpx 10rpx #ffffff; */
  box-shadow: var(--z-tabbar2-active-item-shadow);
  pointer-events: none;
  transition: left 0.3s cubic-bezier(0.645, 0.045, 0.355, 1),
              width 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
  /* 高度、宽度、left 由内联样式覆盖 */
}
</style>