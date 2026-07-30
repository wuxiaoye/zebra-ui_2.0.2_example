<template>
  <!-- 外层容器：控制布局、label、禁用，不干扰内部原生radio样式 -->
  <view
    class="aye-radio-wrap"
    :class="[
      finalDisabled ? 'is-disabled' : '',
      finalVerticalFull ? 'vertical-full' : '',
      finalReverseAlign ? 'reverse-align' : ''
    ]"
    @tap="handleTap"
  >
    <!-- 【核心单选圆圈：完全沿用你原始模板+样式，未做任何删减修改】 -->
    <view
      class="aye-radio"
      :class="{ checked: isChecked }"
      :style="{ width: iconSize, height: iconSize }"
    >
      <view
        class="radio-dot"
        :style="{
          width: dotInnerSize,
          height: dotInnerSize,
          backgroundColor: isChecked ? activeColor : normalColor
        }"
      ></view>
    </view>

    <!-- 文字标签 -->
    <text
      v-if="label"
      class="radio-label"
      :style="{
        fontSize: labelSize,
        color: finalDisabled ? disabledTextColor : textColor
      }"
    >
      {{ label }}
    </text>
  </view>
</template>

<script setup>
import { inject, computed } from 'vue'

// 注入group
const groupInject = inject('ayeRadioGroup', null)
const groupBindProps = groupInject?.groupProps || null

const props = defineProps({
  modelValue: {
    type: [String, Number],
    default: ''
  },
  value: {
    type: [String, Number],
    required: true
  },
  label: {
    type: String,
    default: ''
  },
  disabled: {
    type: Boolean,
    default: undefined
  },
  // 自定义尺寸颜色
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
    default: undefined
  },
  // 竖向铺满、反向对齐
  verticalFull: {
    type: Boolean,
    default: undefined
  },
  reverseAlign: {
    type: Boolean,
    default: undefined
  }
})

const emit = defineEmits(['update:modelValue', 'change'])

// ===================== 优先级计算：自身 > group > 默认值 =====================
// 禁用状态
const finalDisabled = computed(() => {
  if (props.disabled !== undefined) return props.disabled
  return groupBindProps?.disabled?.value ?? false
})

// 外框尺寸，内部圆点永远是外框一半（和原始25rpx/50rpx比例一致）
const finalIconSize = computed(() => props.iconSize || groupBindProps?.iconSize?.value || '50rpx')
const dotInnerSize = computed(() => {
  const num = parseInt(finalIconSize.value) / 2
  return `${num}rpx`
})

// 圆点颜色
const activeColor = computed(() => props.iconActiveColor || groupBindProps?.iconActiveColor?.value || '#07c160')
const normalColor = computed(() => props.iconNormalColor || groupBindProps?.iconNormalColor?.value || '#9baacf')

// 文字样式
const textColor = computed(() => props.labelColor || groupBindProps?.labelColor?.value || '#333')
const labelSize = computed(() => props.labelSize || groupBindProps?.labelSize?.value || '32rpx')
const disabledTextColor = '#c0c4cc'

// 布局属性
const finalVerticalFull = computed(() => {
  if (props.verticalFull !== undefined) return props.verticalFull
  return groupBindProps?.verticalFull?.value ?? false
})
const finalReverseAlign = computed(() => {
  if (props.reverseAlign !== undefined) return props.reverseAlign
  return groupBindProps?.reverseAlign?.value ?? false
})

// 是否选中
const isChecked = computed(() => {
  if (groupInject) return groupInject.currentValue.value === props.value
  return props.modelValue === props.value
})

// 点击事件
const handleTap = () => {
  if (finalDisabled.value) return

  if (groupInject) {
    groupInject.setCurrent(props.value)
    emit('change', props.value, true)
  } else {
    emit('update:modelValue', props.value)
    emit('change', props.value, true)
  }
}
</script>

<style scoped>
/* ========== 你原始完整CSS，一行未删、未改、未精简，原样保留 ========== */
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
  --primary: #07c160;
}
.aye-radio {
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50rpx;
  height: 50rpx;
  border-radius: 50%;
  transition: all 0.3s ease;
}
.aye-radio.checked {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}
.radio-dot {
  width: 25rpx;
  height: 25rpx;
  background-color: var(--greyDark);
  border-radius: 50%;
  transition: 0.3s ease;
}
.aye-radio.checked .radio-dot {
  background-color: var(--primary);
}

/* ========== 新增外层布局、label、禁用样式，不污染原有radio ========== */
.aye-radio-wrap {
  display: flex;
  align-items: center;
  gap: 16rpx;
  cursor: pointer;
}
/* 竖向占满整行两端对齐 */
.aye-radio-wrap.vertical-full {
  width: 100%;
  justify-content: space-between;
}
/* 反向：文字左，圆点右 */
.aye-radio-wrap.reverse-align {
  flex-direction: row-reverse;
}
/* 禁用置灰 */
.aye-radio-wrap.is-disabled {
  opacity: 0.55;
  pointer-events: none;
}
.radio-label {
  flex-shrink: 0;
}
</style>