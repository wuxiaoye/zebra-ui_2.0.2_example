<template>
  <view
    :class="bem({ select: selected, disabled, pulse: pulse })"
    :style="customStyle"
    @click="onClick"
  >
      <template v-if="instance.slots.title">
        <slot name="title"></slot>
      </template>
      <template v-else>
          <view class="content-wrap">
                <z-badge v-bind="badgeProps" :dot="dot" :content="badge">
                      <z-icon :name="props.icon" :size="props.iconSize" 
                        :color="disabled ? 'var(--z-sidebar-disabled-text-color)' : ( selected ? props.activeIconColor :  props.iconColor) "
                        ></z-icon>
                </z-badge>
              <text class="title-text">{{ title }}</text>
          </view>
      </template>
  </view>
</template>

<script setup lang="ts">
import { computed, getCurrentInstance, ref } from 'vue'
import {
  numericProp,
  createNamespace,
  useParent,
  useComponentName
} from '../../libs/utils'
import zBadge from '../z-badge/z-badge.vue'

const instance = getCurrentInstance()!
const [componentName, bem] = createNamespace('sidebar-item')
useComponentName(componentName)

const props = defineProps({
  dot: Boolean,
  title: String,
  badge: numericProp,
  disabled: Boolean,
  badgeProps: Object,
  customStyle: {
    type: Object,
    default: () => {}
  },
  icon:{
      type: String,
      default: 'home'
  },
  iconSize:{
      type: String,
      default: '36rpx'
  },
  iconColor:{
      type: String,
      default: 'var(--greyDark)'
  },
  activeIconColor:{
      type: String,
      default: 'var(--white)'
  },
})
const emit = defineEmits(['click'])
// @ts-ignore
const { parent, index } = useParent('z-sidebar')
const selected = computed(() => index.value === parent.getActive())

const pulse = ref(false)

const onClick = () => {
  if (props.disabled) {
    return
  }
  emit('click', index.value)
  parent.setActive(index.value)

  pulse.value = true
  // 动画执行完，关掉class，动画总共0.4s
  setTimeout(()=>{
    pulse.value = false
  },400)
}
</script>

<script lang="ts">
export default {
  name: 'ZSidebarItem',
  options: {
    virtualHost: true
  }
}
</script>

<style lang="scss" scoped>
.z-sidebar-item {
  position: relative;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  color: var(--z-sidebar-text-color);
  background: var(--z-sidebar-background);
  transition: all 0.4s ease;
  
  .content-wrap{
      display: flex;
      flex-direction: column;
      flex: 1;
      justify-content: center;
      align-items: center;
      padding: var(--z-sidebar-padding);
  }
  .title-text{
      font-size: var(--z-sidebar-font-size);
      margin-top: 14rpx;
      line-height: var(--z-sidebar-text-line-height);
      transition: all 0.4s ease;
  }

  &:not(:last-child)::after {
    // border-bottom-width: 1px;
  }

  &__text {
    word-break: break-all;
  }

  &--select {
    font-weight: var(--z-sidebar-selected-font-weight);
    color: var(--z-sidebar-selected-text-color);
    background: var(--z-sidebar-selected-background);
    border-radius: var(--z-sidebar-selected-border-radius);
  }

  // 点击脉冲上浮回落动画：0~0.2s向上，0.2~0.4s落回去
  &--pulse {
    animation: pulseUp 0.4s ease-out;
  }

  &--disabled {
    color: var(--z-sidebar-disabled-text-color);
    cursor: not-allowed;

    &:active {
      background-color: var(--z-sidebar-background);
    }
  }
}

@keyframes pulseUp {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-4px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>