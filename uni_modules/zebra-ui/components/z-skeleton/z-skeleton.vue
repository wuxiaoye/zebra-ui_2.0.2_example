<template>
  <template v-if="!props.loading">
    <slot></slot>
  </template>
  <view
    v-else
    :class="bem({
      animate: props.animate,
      round: props.round,
      'avatar-right': props.avatarRight
    })"
  >
    <template v-if="instance.slots.template">
      <slot name="template"></slot>
    </template>
    <template v-else>
      <!-- 头像 -->
      <template v-if="props.avatar">
        <z-skeleton-avatar
          :avatar-shape="props.avatarShape"
          :avatar-size="props.avatarSize"
        />
      </template>
      <!-- 文本内容区域 -->
      <view :class="bem('content')">
        <template v-if="props.title">
          <z-skeleton-title
            :round="props.round"
            :title-width="props.titleWidth"
          />
        </template>
        <template v-for="(_, index) in Array(+props.row).fill('')" :key="index">
          <z-skeleton-paragraph
            :round="props.round"
            :row-width="addUnit(getRowWidth(index))"
          />
        </template>
      </view>
    </template>
  </view>
</template>

<script lang="ts" setup>
import { type PropType, getCurrentInstance } from 'vue'
import {
  addUnit,
  truthProp,
  numericProp,
  makeStringProp,
  makeNumericProp,
  createNamespace,
  type Numeric,
  useComponentName
} from '../../libs/utils'
import zSkeletonAvatar from '../z-skeleton-avatar/z-skeleton-avatar.vue'
import zSkeletonTitle from '../z-skeleton-title/z-skeleton-title.vue'
import zSkeletonParagraph from '../z-skeleton-paragraph/z-skeleton-paragraph.vue'

type SkeletonAvatarShape = 'square' | 'round'
const [name, bem] = createNamespace('skeleton')
useComponentName(name)
const DEFAULT_LAST_ROW_WIDTH = '60%'

const props = defineProps({
  row: makeNumericProp(0),
  round: Boolean,
  title: Boolean,
  titleWidth: numericProp,
  avatar: Boolean,
  avatarSize: numericProp,
  avatarShape: makeStringProp<SkeletonAvatarShape>('round'),
  // 新增：头像是否展示在右侧
  avatarRight: Boolean,
  loading: truthProp,
  animate: truthProp,
  rowWidth: {
    type: [Number, String, Array] as PropType<Numeric | Numeric[]>,
    default: '100%'
  }
})

const instance = getCurrentInstance()!

const getRowWidth = (index: number) => {
  const { rowWidth } = props
  // @ts-ignore
  if (rowWidth === '100%' && index === +props.row - 1) {
    return DEFAULT_LAST_ROW_WIDTH
  }

  if (Array.isArray(rowWidth)) {
    return rowWidth[index]
  }

  return rowWidth
}
</script>

<script lang="ts">
export default {
  name: 'ZSkeleton',
  options: {
    virtualHost: true
  }
}
</script>

<style lang="scss" scoped>
.z-skeleton {
  display: flex;
  align-items: flex-start;
  gap: 22rpx; // 头像与内容间距

  &__content {
    width: 100%;
  }

  &--animate {
    animation: z-skeleton-blink var(--z-skeleton-duration) ease-in-out infinite;
  }

  // 头像居右修饰类：flex反向排列
  &--avatar-right {
    flex-direction: row-reverse;
  }
}

@keyframes z-skeleton-blink {
  50% {
    opacity: 0.6;
  }
}
</style>