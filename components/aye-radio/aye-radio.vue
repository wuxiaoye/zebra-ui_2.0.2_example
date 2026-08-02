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
    <!-- 【核心单选圆圈：完全沿用你原始模板】 -->
    <view
      class="aye-radio"
      :class="{ checked: isChecked }"
      :style="{
        width: finalIconSize,
        height: finalIconSize
      }"
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

/**
 * 尺寸解析工具：自动兼容 60 / 60rpx / 60px
 * 无单位默认补 rpx，圆点数值对半、单位跟随外圈
 */
function parseSizeStr(str) {
  if (!str) return { num: null, unit: 'rpx' }
  const match = String(str).match(/^(\d+)(rpx|px)?$/)
  if (!match) return { num: null, unit: 'rpx' }
  const num = Number(match[1])
  const unit = match[2] || 'rpx'
  return { num, unit }
}

// 注入group，兜底空对象避免null报错
const groupInject = inject('ayeRadioGroup', null)
const groupBindProps = groupInject?.groupProps ?? {}

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

// 禁用状态 优先级自身 > group
const finalDisabled = computed(() => {
  if (props.disabled !== undefined) return props.disabled
  return groupBindProps.disabled?.value ?? false
})

// 外层最终尺寸
const finalIconSize = computed(() => {
  let raw = props.iconSize
  if (raw === undefined) {
    raw = groupBindProps.iconSize?.value
  }
  return raw || '50rpx'
})

// 圆点尺寸：数值减半，单位和外圈保持一致
const dotInnerSize = computed(() => {
  const { num, unit } = parseSizeStr(finalIconSize.value)
  if (num === null || isNaN(num)) return '25rpx'
  return `${num / 2}${unit}`
})

// 圆点颜色
const activeColor = computed(() => {
  if (props.iconActiveColor !== undefined) return props.iconActiveColor
  return groupBindProps.iconActiveColor?.value ?? '#07c160'
})
const normalColor = computed(() => {
  if (props.iconNormalColor !== undefined) return props.iconNormalColor
  return groupBindProps.iconNormalColor?.value ?? '#9baacf'
})

// 文字样式
const textColor = computed(() => {
  if (props.labelColor !== undefined) return props.labelColor
  return groupBindProps.labelColor?.value ?? '#333'
})
const labelSize = computed(() => {
  if (props.labelSize !== undefined) return props.labelSize
  return groupBindProps.labelSize?.value ?? '32rpx'
})
const disabledTextColor = '#666'

// 布局属性
const finalVerticalFull = computed(() => {
  if (props.verticalFull !== undefined) return props.verticalFull
  return groupBindProps.verticalFull?.value ?? false
})
const finalReverseAlign = computed(() => {
  if (props.reverseAlign !== undefined) return props.reverseAlign
  return groupBindProps.reverseAlign?.value ?? false
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
/* ========== 完全还原你最初原始CSS，一行未改动 ========== */
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
  --primary: #07c160;
}
/* 定义回弹动画：先缩小，0.7秒后恢复原状 */
@keyframes radioDotBounce {
  0% {
    transform: scale(1);
  }
  35% {
    transform: scale(0.85);
  }
  100% {
    transform: scale(1);
  }
}
.aye-radio {
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50rpx;
  height: 50rpx;
  border-radius: 50%;
  transition: all 0.4s ease;
}
.aye-radio.checked {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}
.radio-dot {
  width: 25rpx;
  height: 25rpx;
  background-color: var(--greyDark);
  border-radius: 50%;
    transform: scale(1);
  transition: all 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
}
.aye-radio.checked .radio-dot {
  background-color: var(--primary);
  /* transform: scale(0.85); */
  animation: radioDotBounce 0.6s ease forwards;
}

/* ========== 外层布局、label、禁用样式原样保留 ========== */
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


.aye-radio-wrap.is-disabled .radio-dot {
  background-color: var(--greyLight-2) !important;
}
.radio-label {
  flex-shrink: 0;
}
</style>