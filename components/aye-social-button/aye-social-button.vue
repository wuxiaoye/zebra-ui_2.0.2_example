<template>
  <view 
    class="aye-plain-button" 
    :class="{ active: modelValue, 'has-text': !!text }" 
    :style="cssVars"
    @tap="toggle"
  >
    <!-- 图标文字统一套一层容器，提高层级 -->
    <view class="btn-inner">
      <uv-icon 
        v-if="icon"
        :name="icon" 
        :color="modelValue ? activeIconColor : iconColor"
      ></uv-icon>
      <text v-if="text" class="btn-text">{{ text }}</text>
    </view>
  </view>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  // 原有配置
  icon: { type: String, default: 'home-fill' }, //图标
  iconColor: { type: String, default: '#9baacf' }, //图标颜色
  activeIconColor: { type: String, default: '#ffffff' }, //激活状态-图标颜色
  activeBgColor: { type: String, default: '#07c160' }, //激活状态-背景颜色
  modelValue: { type: Boolean, default: false }, //传递的值, 按钮是否被激活
  round: { type: Boolean, default: false }, //是否圆形按钮
  radius: { type: String, default: '' }, //自定义圆角

  // 按钮尺寸
  width: { type: String, default: '' },
  height: { type: String, default: '' },

  // 文字相关
  text: { type: String, default: '' }, //文字
  textColor: { type: String, default: '#666' }, //文字颜色
  activeTextColor: { type: String, default: '#fff' } //激活状态-文字颜色
});
const emit = defineEmits(['update:modelValue', 'click']);

const cssVars = computed(() => {
  // 圆角优先级逻辑
  let btnRadius = '10px';
  if (props.round) {
    btnRadius = '9999px';
  } else if (props.radius) {
    btnRadius = props.radius;
  }

  return {
    '--active-bg': props.activeBgColor,
    '--btn-radius': btnRadius,
    '--btn-width': props.width,
    '--btn-height': props.height,
    '--text-color': props.textColor,
    '--active-text-color': props.activeTextColor
  };
});

const toggle = () => {
  emit('update:modelValue', !props.modelValue);
  emit('click');
};
</script>

<style scoped>
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
}
.aye-plain-button {
  box-sizing: border-box;
  border-radius: var(--btn-radius);
  width: var(--btn-width, auto);
  height: var(--btn-height, auto);
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  box-shadow: 3px 3px 6px #c8d0e7, -2px -2px 5px #FFFFFF;
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}
/* 有文字 + 激活态：按钮自身铺满背景色 */
.aye-plain-button.has-text.active {
  background-color: var(--active-bg);
}
/* 无文字时激活态保持透明，靠伪元素填充 */
.aye-plain-button:not(.has-text).active {
  background-color: transparent;
}
/* 图标文字容器，层级高于伪元素 */
.btn-inner {
  display: flex;
  gap: 6px;
  align-items: center;
  position: relative;
  z-index: 2;
}
.btn-text {
  font-size: 14px;
  color: var(--text-color);
  transition: color 0.35s;
}
.aye-plain-button.active .btn-text {
  color: var(--active-text-color);
}
/* 伪元素：有文字直接隐藏 */
.aye-plain-button.has-text::before {
  display: none;
}
/* 无文字时显示伪元素动画 */
.aye-plain-button:not(.has-text)::before {
  content: "";
  width: 120%;
  height: 120%;
  position: absolute;
  top: 90%;
  left: -110%;
  transform: rotate(45deg);
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
  background-color: var(--active-bg, #00e600);
  z-index: 1;
}
.aye-plain-button:not(.has-text).active::before {
  top: -10%;
  left: -10%;
}
</style>