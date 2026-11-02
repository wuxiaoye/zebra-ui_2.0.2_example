<template>
  <!-- 宽度测量占位符 -->
  <view class="aye-text-ellipsis-ph" style="width: 100%"></view>

  <!-- 主渲染容器 -->
  <view class="aye-text-ellipsis" :style="customStyle">
    <template v-if="expanded">
      {{ props.content }}
    </template>
    <template v-else>
      {{ text }}
    </template>
    <template v-if="hasAction">
      <view class="aye-text-ellipsis__action" @click="onClickAction">
        <template v-if="instance.slots.action">
          <slot name="action" :expanded="expanded"></slot>
        </template>
        <template v-else>
          {{ actionText }}
        </template>
      </view>
    </template>
  </view>

  <!-- 高度测量克隆节点 -->
  <view
    v-if="cloneContainerShow"
    class="aye-text-ellipsis-rect aye-text-ellipsis"
    :style="{ ...cloneContainerStyle, ...customStyle }"
  >
    {{ cloneContainerText }}
  </view>
</template>

<script lang="ts" setup>
import {
  ref,
  watch,
  computed,
  onMounted,
  getCurrentInstance,
  nextTick
} from 'vue'
import {
  makeNumericProp,
  makeStringProp,
  windowWidth,
  useExpose,
  getRect,
  raf,
  addUnit,
  useComponentName
} from '../../libs/utils'

useComponentName('aye-text-ellipsis')

const instance = getCurrentInstance()!

const props = defineProps({
  rows: makeNumericProp(1),
  dots: makeStringProp('...'),
  content: makeStringProp(''),
  expandText: makeStringProp(''),
  collapseText: makeStringProp(''),
  position: makeStringProp('end'),
  customStyle: Object
})

const emit = defineEmits(['clickAction'])

const text = ref('')
const expanded = ref(false)
const hasAction = ref(false)

const actionText = computed(() =>
  expanded.value ? props.collapseText : props.expandText
)

/**
 * 尺寸单位解析：自动识别 px/rpx，统一转换为 px 数值
 * 无单位时默认按 rpx 处理，兼容原组件使用习惯
 */
const parseSizeToPx = (value: string | number | undefined | null): number => {
  if (value === undefined || value === null || value === '') return 0
  const str = String(value)
  const numMatch = str.match(/^(\d+(\.\d+)?)/)
  if (!numMatch) return 0
  
  const num = Number(numMatch[1])
  const unit = str.slice(numMatch[0].length).toLowerCase() || 'rpx'

  if (unit === 'px') return num
  if (unit === 'rpx') return uni.upx2px(num)
  return num
}

const cloneContainerShow = ref(false)
const cloneContainerStyle = ref({}) as any
const cloneContainerText = ref('')

const calcEllipsised = () => {
  const cloneContainer = (width: number) => {
    cloneContainerStyle.value.position = 'fixed'
    cloneContainerStyle.value.zIndex = '-9999'
    cloneContainerStyle.value.top = '-19998rpx'
    cloneContainerStyle.value.height = 'auto'
    cloneContainerStyle.value.width = addUnit(width)
    cloneContainerStyle.value.minHeight = 'auto'
    cloneContainerStyle.value.maxHeight = 'auto'
    cloneContainerText.value = props.content
    cloneContainerShow.value = true
    return cloneContainerStyle.value
  }

  const calcEllipsisText = (container: any, maxHeight: number) => {
    return new Promise((resolve) => {
      const { content, position, dots }: any = props
      const end = content.length
      // 按钮前加空格，模拟实际间距，确保测量和渲染一致
      const actionGap = ' '

      const calcEllipse = () => {
        return new Promise((resolve0) => {
          const tail = (left: number, right: number) => {
            return new Promise((resolve1) => {
              if (right - left <= 1) {
                if (position === 'end') {
                  resolve1(content.slice(0, left) + dots)
                  return
                }
                resolve1(dots + content.slice(right, end))
                return
              }

              const middle = Math.round((left + right) / 2)
              // 截断文本时包含：正文 + 省略号 + 间距 + 按钮文本
              if (position === 'end') {
                cloneContainerText.value =
                  content.slice(0, middle) + dots + actionGap + actionText.value
              } else {
                cloneContainerText.value =
                  dots + content.slice(middle, end) + actionGap + actionText.value
              }
              raf(() => {
                getRect(instance, '.aye-text-ellipsis-rect').then((res: any) => {
                  const { height } = res
                  if (height > maxHeight) {
                    if (position === 'end') {
                      resolve1(tail(left, middle))
                      return
                    }
                    resolve1(tail(middle, right))
                    return
                  }
                  if (position === 'end') {
                    resolve1(tail(middle, right))
                    return
                  }
                  resolve1(tail(left, middle))
                  return
                })
              })
            })
          }
          tail(0, end).then((value) => {
            cloneContainerText.value = value as string
            resolve0(value)
          })
        })
      }

      const middleTail = (
        leftPart: [number, number],
        rightPart: [number, number]
      ) => {
        return new Promise((resolveMiddle) => {
          if (
            leftPart[1] - leftPart[0] <= 1 &&
            rightPart[1] - rightPart[0] <= 1
          ) {
            resolveMiddle(
              content.slice(0, leftPart[0]) +
                dots +
                content.slice(rightPart[1], end)
            )
            return
          }

          const leftMiddle = Math.floor((leftPart[0] + leftPart[1]) / 2)
          const rightMiddle = Math.ceil((rightPart[0] + rightPart[1]) / 2)

          cloneContainerText.value =
            props.content.slice(0, leftMiddle) +
            props.dots +
            actionGap +
            props.content.slice(rightMiddle, end) +
            props.expandText

          raf(() => {
            getRect(instance, '.aye-text-ellipsis-rect').then((res: any) => {
              const { height } = res
              if (height >= maxHeight) {
                resolveMiddle(
                  middleTail(
                    [leftPart[0], leftMiddle],
                    [rightMiddle, rightPart[1]]
                  )
                )
                return
              }
              resolveMiddle(
                middleTail(
                  [leftMiddle, leftPart[1]],
                  [rightPart[0], rightMiddle]
                )
              )
              return
            })
          })
        })
      }

      const middle = (0 + end) >> 1
      if (props.position === 'middle') {
        middleTail([0, middle], [middle, end]).then((res0: any) => {
          cloneContainerText.value = res0
          resolve(res0)
          return
        })
      } else {
        calcEllipse().then((res1) => {
          resolve(res1)
          return
        })
      }
    })
  }

  raf(() => {
    getRect(instance, '.aye-text-ellipsis-ph').then((result: any) => {
      const container = cloneContainer(result.width)
      if (!container) return
      if (!props.customStyle || !props.customStyle['font-size']) {
        console.warn('[Aye] 请通过customStyle设置font-size！')
        return
      }

      // 全量尺寸走单位解析，支持 px / rpx 混合使用
      const paddingTop = parseSizeToPx(props.customStyle.paddingTop)
      const paddingBottom = parseSizeToPx(props.customStyle.paddingBottom)
      const fontSize = props.customStyle['font-size']
      let lineHeight = props.customStyle['line-height']

      // 未传行高时，基于解析后的字号自动计算
      if (!lineHeight && lineHeight !== 0) {
        const fontSizePx = parseSizeToPx(fontSize)
        lineHeight = 1.6 * fontSizePx
      } else {
        lineHeight = parseSizeToPx(lineHeight)
      }

      // 严格按指定行数计算最大高度，无多余余量
      const maxHeight = Math.ceil(
        Number(props.rows) * lineHeight + paddingTop + paddingBottom
      )

      nextTick(() => {
        raf(() => {
          getRect(instance, '.aye-text-ellipsis-rect').then((res: any) => {
            if (maxHeight < res.height) {
              hasAction.value = true
              calcEllipsisText(container, maxHeight).then((res: string) => {
                text.value = res
                cloneContainerShow.value = false
              })
            } else {
              hasAction.value = false
              text.value = props.content
              cloneContainerShow.value = false
            }
          })
        })
      })
    })
  })
}

const toggle = (isExpanded = !expanded.value) => {
  expanded.value = isExpanded
}

const onClickAction = (event: any) => {
  toggle()
  emit('clickAction', event)
}

onMounted(calcEllipsised)

watch(
  [windowWidth, () => [props.content, props.rows, props.position]],
  calcEllipsised
)

useExpose({ toggle })
defineExpose({ toggle })
</script>

<script lang="ts">
export default {
  name: 'AyeTextEllipsis',
  options: {
    virtualHost: true
  }
}
</script>

<style lang="scss" scoped>
.aye-text-ellipsis {
  line-height: 1.6;
  overflow-wrap: break-word;
  white-space: pre-wrap;
  word-break: break-all;
  position: relative;

  &__action {
    display: inline-block;
    color: #07c160;
    cursor: pointer;
    white-space: nowrap; /* 强制按钮文字不换行 */
    margin-left: 4rpx;
    vertical-align: baseline;

    &:active {
      opacity: 0.7;
    }
  }
}

/* 测量用克隆节点，和主容器样式保持一致 */
.aye-text-ellipsis-rect {
  pointer-events: none;
  visibility: hidden;
}
</style>
