<template>
  <!-- 普通按钮（primary / secondary） -->
  <view v-if="type === 'primary' || type === 'secondary'" 
        class="aye-btn" 
        :class="[`btn__${type}`, `btn-size--${size}`]" 
        :style="btnStyle"
        @tap="$emit('click')">
    <text :style="fontStyle">{{ label }}</text>
  </view>

  <!-- 斜向上动画按钮 -->
  <view v-else-if="type === 'change-up'" 
        class="aye-change-button background-color-zi btn-text-hui" 
        :class="{ active: modelValue, [`btn-size--${size}`]: true }" 
        :style="btnStyle"
        @tap="toggle">
    <text class="button-content" :style="fontStyle">{{ label }}</text>
  </view>

  <!-- 从下往上动画按钮 -->
  <view v-else-if="type === 'change-upward'" 
        class="aye-change-button ani-upward background-color-zi btn-text-hui" 
        :class="{ active: modelValue, [`btn-size--${size}`]: true }" 
        :style="btnStyle"
        @tap="toggle">
    <text class="button-content" :style="fontStyle">{{ label }}</text>
  </view>

  <!-- 颜色渲染动画按钮 -->
  <view v-else-if="type === 'change-color'" 
        class="aye-change-color-button" 
        :class="{ active: modelValue, [`btn-size--${size}`]: true }" 
        :style="btnStyle"
        @tap="toggle">
    <text class="button-content" :style="fontStyle">{{ label }}</text>
  </view>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  type: { 
    type: String, 
    default: 'primary', 
    validator: val => ['primary','secondary','change-up','change-upward','change-color'].includes(val)
  },
  size: {
    type: String,
    default: 'normal',
    validator: val => ['mini','small','normal','large'].includes(val)
  },
  label: { type: String, default: '空白按钮' },
  modelValue: { type: Boolean, default: false },

  // 自定义内边距，格式同css padding：'10px' / '10px 20px' 等
  customPadding: {
    type: String,
    default: ''
  },
  // 自定义字号，如 '16px'
  customFontSize: {
    type: String,
    default: ''
  },
  // 自定义圆角，如 '8px'
  customRadius: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['update:modelValue', 'click'])

const toggle = () => {
  emit('update:modelValue', !props.modelValue)
  emit('click')
}

// 按钮容器样式：padding + border-radius
const btnStyle = computed(() => {
  const styleObj = {}
  if (props.customPadding) styleObj.padding = props.customPadding
  if (props.customRadius) styleObj.borderRadius = props.customRadius
  return styleObj
})

// 文字字号样式
const fontStyle = computed(() => {
  const fontObj = {}
  if (props.customFontSize) fontObj.fontSize = props.customFontSize
  return fontObj
})
</script>

<style scoped>
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
  --primary-light: #34ff6a;
  --primary: #08e670;
  --primary-dark: #07c160;
}

/* ========== 尺寸统一配置（4种规格，已转为 px） ========== */
/* mini 超小 */
.btn-size--mini {
  font-size: 12px !important;
}
.aye-change-button.btn-size--mini,
.aye-change-color-button.btn-size--mini ,
.aye-btn.btn-size--mini {
  padding: 5px 10px;
  border-radius: 6px;
}

/* small 小号 */
.btn-size--small {
  font-size: 13px !important;
}
.aye-change-button.btn-size--small,
.aye-change-color-button.btn-size--small ,
.aye-btn.btn-size--small {
  padding: 7px 15px;
  border-radius: 8px;
}

/* normal 默认标准尺寸 */
.btn-size--normal {
  font-size: 15px !important;
}
.aye-change-button.btn-size--normal,
.aye-change-color-button.btn-size--normal ,
.aye-btn.btn-size--normal {
  padding: 10px 40px;
  border-radius: 8px;
}

/* large 大号 */
.btn-size--large {
  font-size: 17px !important;
}
.aye-change-button.btn-size--large,
.aye-change-color-button.btn-size--large ,
.aye-btn.btn-size--large {
  padding: 13px 50px;
  border-radius: 10px;
}

/* ========== 通用普通按钮 ========== */
.aye-btn {
  box-shadow: 3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
  justify-self: center;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}
.aye-btn.btn__primary {
  background: var(--primary);
  box-shadow: inset 2px 2px 10px var(--primary-light), inset -2px -2px 10px var(--primary-dark), 3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
  color: #fff;
}
.aye-btn.btn__secondary {
  color: var(--greyDark);
}
.aye-btn:active {
  box-shadow: inset 2px 2px 5px var(--greyLight-2), inset -2px -2px 5px var(--white);
  color: var(--primary);
}
.aye-btn.btn__primary:active {
  box-shadow: inset 2px 2px 10px var(--primary-dark), inset -2px -2px 10px var(--primary-light);
  color: var(--primary-light);
}

/* ========== 动画按钮（斜向上） ========== */
.aye-change-button {
  box-shadow: 3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}
.aye-change-button .button-content {
  z-index: 1;
  position: relative;
  transition: color 0.35s ease;
}
.aye-change-button.btn-text-hui {
  color: var(--greyDark);
}
.aye-change-button::before {
  content: "";
  width: 100%;
  height: 100%;
  position: absolute;
  top: 110%;
  left: -110%;
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}
.aye-change-button.background-color-zi::before {
  background: var(--primary);
  box-shadow: inset 2px 2px 10px var(--primary-light), inset -2px -2px 10px var(--primary-dark), 3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
  color: var(--greyLight-1);
}
.aye-change-button.active::before {
  top: 0%;
  left: 0%;
}
.aye-change-button.active {
  color: #fff !important;
}

/* 从下往上动画 */
.aye-change-button.ani-upward::before {
  top: 110%;
  left: 0%;
}
.aye-change-button.ani-upward.active::before {
  top: 0%;
  left: 0%;
}

/* ========== 纯色切换按钮 ========== */
.aye-change-color-button {
  box-shadow: 3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.35s ease-in-out;
  color: var(--greyDark);
}
.aye-change-color-button .button-content {
  transition: color 0.35s ease-in-out;
}
.aye-change-color-button.active {
  background: var(--primary);
  box-shadow: inset 2px 2px 10px var(--primary-light), inset -2px -2px 10px var(--primary-dark), 3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
  color: var(--white);
}
</style>