<template>
  <view :class="bem()">
    <view :class="bem('image')" :style="getSizeStyle(props.imageSize)">
      <!-- image插槽 -->
      <template v-if="instance.slots.image">
        <slot name="image"></slot>
      </template>
      <!-- iconType字体图标 -->
      <text
        v-else-if="props.iconType"
        :class="['ayeIconfont', iconFontClass]"
        :style="{ fontSize: iconFontSize }"
      />
      <!-- 自定义图片 -->
      <image
        v-else-if="props.image"
        :src="props.image"
        mode="aspectFill"
      ></image>
      <!-- 默认 empty-icon 占位，无插槽、无iconType、无image才显示 -->
      <view v-else class="empty-icon"></view>
    </view>

    <template v-if="instance.slots.description">
      <slot name="description"></slot>
    </template>
    <template v-else>
      <text :class="bem('description')">{{ props.description }}</text>
    </template>

    <template v-if="instance.slots.default">
      <view :class="bem('bottom')">
        <slot></slot>
      </view>
    </template>
  </view>
</template>

<script lang="ts" setup>
import { type PropType, getCurrentInstance, computed, watch } from 'vue'
import {
  type Numeric,
  getSizeStyle,
  makeStringProp,
  createNamespace,
  useComponentName
} from '../../libs/utils'
const [name, bem] = createNamespace('empty')
useComponentName(name)
const instance = getCurrentInstance()!

const props = defineProps({
  image: String,
  //控制 图片的大小
  imageSize: [Number, String, Array] as PropType<Numeric | [Numeric, Numeric]>,
  description: String,
  iconType: {
    type: String as PropType<'default' | 'error' | 'network' | 'search'>,
    default: ''
  },
  //控制 icon 图标的大小
  size: {
    type: [Number, String] as PropType<Numeric>,
    default: '81px'
  }
})

// 旧关键字列表，用于警告
const legacyImageKeywords = ['default', 'error', 'network', 'search']

// 监听 image 属性，出现旧关键字抛出 warn 提示
watch(
  () => props.image,
  (val) => {
    if (val && legacyImageKeywords.includes(val)) {
      console.warn(
        `[ZEmpty warn] image="${val}" 已废弃，请迁移使用 icon-type="${val}"，image 属性现在仅用于传入自定义图片URL`
      )
    }
  },
  { immediate: true }
)

// 映射iconType到字体class
const iconFontClass = computed(() => {
  const map: Record<string, string> = {
    default: 'aye-empty-default',
    error: 'aye-error-default',
    network: 'aye-error-network',
    search: 'aye-empty-search'
  }
  return map[props.iconType] || ''
})

/**
 * 解析尺寸，提取数值和单位
 * 示例：300 → {val:300,unit:'px'}；'300rpx' → {val:300,unit:'rpx'}
 */
function parseSize(val: Numeric) {
  if (typeof val === 'number') {
    return { val, unit: 'px' }
  }
  const match = String(val).match(/^([0-9.]+)([a-zA-Z]*)$/)
  if (match) {
    return {
      val: Number(match[1]),
      unit: match[2] || 'px'
    }
  }
  return { val: 100, unit: 'px' }
}

// icon字体图标字号，使用size属性
const iconFontSize = computed(() => {
  const s = parseSize(props.size)
  return `${s.val}${s.unit}`
})

</script>

<script lang="ts">
export default {
  name: 'ZEmpty',
  options: {
    virtualHost: true
  }
}
</script>

<style lang="scss" scoped>
@font-face {
  font-family: "ayeIconfont";
  src:
       url('data:application/x-font-woff2;charset=utf-8;base64,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') format('woff2');
}

.ayeIconfont {
  font-family: "ayeIconfont" !important;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: var(--greyDark);
}

.aye-error-network:before {
  content: "\e86e";
}

.aye-empty-search:before {
  content: "\e643";
}

.aye-empty-default:before {
  content: "\e616";
}

.aye-error-default:before {
  content: "\e61c";
}

.empty-icon {
  width: 128rpx;
  height: 128rpx;
  border-radius: 50%;
  background: var(--greyLight-1);
  box-shadow: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
}

.z-empty {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--z-empty-padding);

  &__image {
    width: var(--z-empty-image-size);
    height: var(--z-empty-image-size);
    display: flex;
    align-items: center;
    justify-content: center;

    image {
      width: 100%;
      height: 100%;
    }
  }

  &__description {
    padding: var(--z-empty-description-padding);
    margin-top: var(--z-empty-description-margin-top);
    font-size: var(--z-empty-description-font-size);
    line-height: var(--z-empty-description-line-height);
    color: var(--z-empty-description-color);
  }

  &__bottom {
    margin-top: var(--z-empty-bottom-margin-top);
  }
}

.z-theme-dark .z-empty {
  opacity: 0.5;
}
</style>