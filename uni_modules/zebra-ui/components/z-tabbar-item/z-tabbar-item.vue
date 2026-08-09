<template>
  <view
    :class="[
        bem({ 
            active: active, 
            animate: parent.props.animate ,
            background: parent.props.background
            })
        ]"
    :style="{
      color: active ? parent.props.activeColor : parent.props.inactiveColor
    }"
    @click="onClick"
  >
    <z-badge
      :dot="dot"
      :wrapper-style="badgeStyle"
      :content="badge"
      v-bind="props.badgeProps"
    >
      <template v-if="instance.slots.icon">
        <slot name="icon" :active="active"></slot>
      </template>
      <template v-else-if="props.icon">
        <z-icon
          :name="props.icon"
          :custom-style="iconStyle"
          :class-prefix="props.iconPrefix"
        />
      </template>
    </z-badge>
    <view :class="bem('text')">
      <slot></slot>
    </view>
  </view>
</template>
<script lang="ts" setup>
import { computed, getCurrentInstance } from 'vue'
import {
  createNamespace,
  numericProp,
  useParent,
  useComponentName
} from '../../libs/utils'
import zBadge from '../z-badge/z-badge.vue'
import zIcon from '../z-icon/z-icon.vue'

const [componentName, bem] = createNamespace('tabbar-item')
useComponentName(componentName)

const instance = getCurrentInstance()!

const props = defineProps({
  dot: Boolean,
  icon: String,
  name: numericProp,
  badge: numericProp,
  badgeProps: Object,
  iconPrefix: String
})

const emit = defineEmits(['click'])
// @ts-ignore
const { parent, index } = useParent('z-tabbar')

const active = computed(() => {
  const { modelValue } = parent.props
  return (props.name ? props.name : index.value) === modelValue
})

const onClick = (event: any) => {
  if (!active.value) {
    parent.setActive(props.name ? props.name : index.value, index, () => {})
  }
  emit('click', event)
}

const badgeStyle = computed(() => {
  const styles = {
    'margin-bottom': 'var(--z-tabbar-item-icon-margin-bottom)',
    'font-size': 'var(--z-tabbar-item-icon-size)'
  }
  return { ...styles }
})

const iconStyle = computed(() => {
  const styles = {
    display: 'block'
  }
  return { ...styles }
})
</script>
<script lang="ts">
export default {
  name: 'ZTabbarItem',
  options: {
    virtualHost: true
  }
}
</script>
<style lang="scss" scoped>
/*  动画：放大 + 弹跳*/
@keyframes bump {
  25% {
      transform: scale(1.35) rotate(8deg);
    }
    50% {
      transform: scale(0.9) rotate(0deg);
    }
    75% {
      transform: scale(1.15) rotate(5deg);
    }
    100% {
      transform: scale(1) rotate(0deg);
    }
}

.z-tabbar-item {
  position: relative;
  z-index: 10;
  display: flex;
  flex: 1;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: var(--z-tabbar-item-font-size);
  line-height: var(--z-tabbar-item-line-height);
  color: var(--z-tabbar-item-text-color);
  transition: all 0.2s ease;

  &--active {
    color: var(--z-tabbar-item-active-color);
    animation: bump 0.3s;
  }
  
  // animate模式 pulse
    // &--active.z-tabbar-item--animate {
    //   animation: pulse 0.5s ease-in-out;
    // }
    
    // =====================
      // ✅ 优先级更高：开启background并且active，强制使用shake，覆盖 bump / pulse
      // =====================
      &--background.z-tabbar-item--active {
        animation: tabShake 0.3s ease-in-out;
      }
}

.z-tabbar-item--active.z-tabbar-item--animate {
  animation: pulse 0.5s ease-in-out;
}

/*  动画：放大*/
@keyframes pulse {
  0% {
    transform: scale3d(1, 1, 1);
  }

  50% {
    transform: scale3d(1.2, 1.2, 1.2);
  }

  100% {
    transform: scale3d(1, 1, 1);
  }
}

// ==========新增：左右摇晃关键帧==========
/*  动画：左右摇晃 */
@keyframes tabShake  {
  0% { transform: translateX(0); }
  20% { transform: translateX(-4px); }
  40% { transform: translateX(4px); }
  60% { transform: translateX(-3px); }
  80% { transform: translateX(3px); }
  100% { transform: translateX(0); }
}

</style>
