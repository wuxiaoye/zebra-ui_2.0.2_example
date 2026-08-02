<template>
  <!-- 复选框外层容器，绑定禁用、布局、反转样式类 -->
  <view
    class="aye-checkbox-wrap"
    :class="[
      { 'is-disabled': finalDisabled },
      { 'is-vertical': finalLayout === 'vertical' },
      { 'vertical-full': finalLayout === 'vertical' && finalVerticalFull },
      { 'vertical-full-reverse': finalLayout === 'vertical' && finalVerticalFull && finalReverseVerticalFull }
    ]"
    @tap="handleClick"
  >
      <view class="aye-checkbox-box">
        <!-- 图标容器 -->
        <view
          class="aye-checkbox"
          :class="[
            { checked: isChecked },
            shapeClass
          ]"
          :style="{
            width: finalIconSize,
            height: finalIconSize
          }"
        >
          <text
            class="ayeIconfont check-icon aye-icon-checkbox-mark"
            :style="{
              fontSize: finalIconSize,
              color: isChecked ? finalActiveIconColor : finalInactiveIconColor
            }"
          ></text>
        </view>

        <!-- 文本标签，无label不渲染 -->
        <text
          v-if="label"
          class="aye-checkbox-label"
          :style="{
            fontSize: finalLabelSize,
            color: finalLabelColor
          }"
        >
          {{ label }}
        </text>
        </view>
  </view>
</template>

<script setup>
import { inject, computed, watch, onMounted, onUnmounted } from 'vue'

// 注入父级group实例
const groupInject = inject('ayeCheckboxGroup', null)
const groupGlobalProps = groupInject?.groupGlobalProps || null

/**
 * 组件入参定义
 */
const props = defineProps({
  // 单独使用时 v-model 绑定布尔值
  modelValue: {
    type: Boolean,
    default: false
  },
  // 在group组内的唯一标识值
  value: {
    type: [String, Number, Boolean],
    default: ''
  },
  // 显示文字
  label: {
    type: String,
    default: ''
  },
  // 自身是否禁用，优先级高于group全局禁用
  disabled: {
    type: Boolean,
    default: undefined
  },
  shape: {
    type: String,
    default: undefined
  },
  activeIconColor: {
    type: String,
    default: undefined
  },
  inactiveIconColor: {
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
  iconSize: {
    type: String,
    default: undefined
  },
  layout: {
    type: String,
    default: undefined
  },
  verticalFull: {
    type: Boolean,
    default: undefined
  },
  reverseVerticalFull: {
    type: Boolean,
    default: undefined
  }
})

/**
 * 对外抛出事件
 * update:modelValue 用于v-model双向绑定
 * change 单个选项变更事件：(当前value, 是否选中)
 */
const emit = defineEmits(['update:modelValue', 'change'])

// ===================== 参数优先级计算：自身props > group全局 > 默认兜底 =====================
const finalDisabled = computed(() => {
  if (props.disabled !== undefined) return props.disabled
  return groupGlobalProps?.disabled?.value ?? false
})

const finalShape = computed(() => {
  if (props.shape !== undefined) return props.shape
  return groupGlobalProps?.shape?.value ?? 'square'
})

const finalActiveIconColor = computed(() => {
  if (props.activeIconColor) return props.activeIconColor
  return groupGlobalProps?.activeIconColor?.value ?? '#07c160'
})

const finalInactiveIconColor = computed(() => {
  if (props.inactiveIconColor) return props.inactiveIconColor
  return groupGlobalProps?.inactiveIconColor?.value ?? '#bbd0f9'
})

const finalLabelColor = computed(() => {
  if (props.labelColor) return props.labelColor
  return groupGlobalProps?.labelColor?.value ?? '#333'
})

const finalLabelSize = computed(() => {
  if (props.labelSize) return props.labelSize
  return groupGlobalProps?.labelSize?.value ?? '32rpx'
})

const finalIconSize = computed(() => {
  if (props.iconSize) return props.iconSize
  return groupGlobalProps?.iconSize?.value ?? '40rpx'
})

const finalLayout = computed(() => {
  if (props.layout) return props.layout
  return groupGlobalProps?.layout?.value ?? 'horizontal'
})

const finalVerticalFull = computed(() => {
  if (props.verticalFull !== undefined) return props.verticalFull
  return groupGlobalProps?.verticalFull?.value ?? false
})

const finalReverseVerticalFull = computed(() => {
  if (props.reverseVerticalFull !== undefined) return props.reverseVerticalFull
  return groupGlobalProps?.reverseVerticalFull?.value ?? false
})

// 形状class
const shapeClass = computed(() => {
  return finalShape.value === 'circle' ? 'shape-circle' : 'shape-square'
})

// 是否勾选
const isChecked = computed(() => {
  if (groupInject) {
    return groupInject.innerValue.value.includes(props.value)
  }
  return props.modelValue
})

// ===================== 向父group上报当前项value与禁用状态（用于全选过滤禁用） =====================
onMounted(() => {
  if (groupInject?.registerOption) {
    groupInject.registerOption(props.value, finalDisabled.value)
  }
})
onUnmounted(() => {
  if (groupInject?.unregisterOption) {
    groupInject.unregisterOption(props.value)
  }
})
// 禁用状态动态变化同步更新
watch(finalDisabled, (newVal) => {
  if (groupInject?.registerOption) {
    groupInject.registerOption(props.value, newVal)
  }
})

/**
 * 点击切换逻辑
 */
const handleClick = () => {
  // 禁用直接拦截
  if (finalDisabled.value) return

  // 存在父级group，交由组统一处理
  if (groupInject) {
    groupInject.handleItemChange(props.value)
    // 单个框抛出change事件
    emit('change', props.value, !isChecked.value)
  } else {
    // 独立使用，自身v-model更新
    const newChecked = !props.modelValue
    emit('update:modelValue', newChecked)
    emit('change', props.value, newChecked)
  }
}
</script>

<style scoped>
:root {
  --greyLight-2: #c8d0e7;
  --white: #FFFFFF;
}

/* 内嵌勾选字体图标 */
@font-face {
  font-family: "ayeIconfont";
  src: url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAAK8AAsAAAAABqAAAAJxAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHFQGYACCcApwdwE2AiQDCAsGAAQgBYULBzcb3gURFYxNsi8O7GbOb0JQKsYR/CA6h66mwsG+j4fv96Od+9/bXUTck2klmWTRyNAhQxdr6omZ7/tuhlL3IgxTYm/b6Uv5bZnhhbCsusQjDa+vw4obn7imfuLTg0TN59JNnVS0pgeb5XnStMM2GuGGMPApyO4I1JKfEaihnzGKSbdZi9TZZfbu0ULmtAZ5Yexqtq5XTQ7JMs1WEyrRvVmcUUFxqniC0/Hn47MBUY1CReKUzNsyeZOH7ya7C9LJ8iTplZPLVdHHClQgoRcysag/NUcSbXhSw5V1oOVZ8G5yWYZOcWibkP46J78WaEXlz6TwlY+aLeCxhmqDTpPOIdqsXHyg6eWmtxpfbHy1295GF1yRJjd7rGhySdKiuSf+lKM3v59X3Hr6qP7np1Q14+9K/w5q/H/x0GnNW/UYde0H40D5I71NtQWCcv6gl+qO+lutZgbv9j+/GgfKHxnmodr+XMHPMawCBbMZociXkIvaQq46n7aGG6Xk+Bp4M9Xc8CZyoaaGE8xVkzNJTZ1zMKP9wAp0JFiJTmFr6Gm+bLHFRyWRq6OL05QNTTxgC3U8ZpMmnoMZ/Q5UYFEBVqIt2RoESyI/r6Yu8SwwipqqgxrLo/Myag48tcEv+KU3UqumxA8yN+2UJ1lL9o4RMt+GefWFqiMnPNBNegx9zzQJt7CaBNWpTFPX9pbE8hCdCTAU1EjlQBoWG7lwOmUc4Gl8zwt4i54h/U1Q8R8Qs2YyJJfIMPCuH9G6B3xltvIKSjnEEWxAbtNmQa/HyNQ+qwWWSoQJiUkpdYUcqk+2Nw4/uw9qcCxFuFcktTcG2K7iPR6MdFEEAA==') format('woff2');
}
.ayeIconfont {
  font-family: "ayeIconfont" !important;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
}
.aye-icon-checkbox-mark:before {
  content: "\e645";
}

/* 默认横向排布 */
.aye-checkbox-wrap {
  display: flex;
  flex-direction: row;
}
.aye-checkbox-box{
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 16rpx;
    cursor: pointer;
}
/* 上下竖向排布 */
.aye-checkbox-wrap.is-vertical {
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
}
.aye-checkbox-wrap.is-vertical .aye-checkbox-box{
    flex-direction: row;
}

/* 竖向撑满整行两端对齐 */
.aye-checkbox-wrap.vertical-full .aye-checkbox-box{
  width: 100%;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
/* 反转左右：文字左，勾选框右 */
.aye-checkbox-wrap.vertical-full-reverse .aye-checkbox-box{
  flex-direction: row-reverse;
}
/* 禁用样式 */
.aye-checkbox-wrap.is-disabled {
  opacity: 0.6;
  pointer-events: none;
}

/* 勾选框外凸阴影 */
.aye-checkbox {
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: box-shadow 0.3s ease;
  flex-shrink: 0;
  padding: 2px;
}
.aye-checkbox.shape-square {
  border-radius: 10rpx;
}
.aye-checkbox.shape-circle {
  border-radius: 50%;
}
/* 选中内凹阴影 */
.aye-checkbox.checked {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}

/* .check-icon, */
 .aye-checkbox-label {
  transition: all 0.3s ease;
}
.check-icon{
  transition: all 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
    transform: scale(1);
}
.aye-checkbox.checked .check-icon{
    transform: scale(0.85);
}

</style>