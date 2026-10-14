<template>
  <view class="asc" :style="{ width: width, height: height, perspective: perspective + 'px' , backgroundColor : backgroundColor, overflow: isOverflowHidden ? 'hidden' : 'visible' }">
    <!-- 3D 场景 -->
    <view
      class="asc__stage"
      @touchstart="onTouchStart"
      @touchmove="onTouchMove"
      @touchend="onTouchEnd"
      @touchcancel="onTouchEnd"
    >
      <view class="asc__cube" :style="cubeStyle">
        <view
          v-for="(item, index) in list"
          :key="index"
          class="asc__face"
          :style="faceStyle(index)"
          @click="onFaceClick(index)"
        >
          <slot name="slide" :item="item" :index="index" :active="index === currentIndex">
            <view class="asc__face-default">Slide {{ index + 1 }}</view>
          </slot>
        </view>
      </view>
    </view>
    <!-- 指示器 -->
    <view v-if="showIndicators" class="asc__dots">
      <view
        v-for="(item, index) in list"
        :key="index"
        class="asc__dot"
        :class="{ 'asc__dot--active': index === currentIndex }"
        @click="slideTo(index)"
      />
    </view>
  </view>
</template>

<script>
export default {
  name: 'AyeSwiperCube',
  props: {
    list: { type: Array, default: () => [] },
    modelValue: { type: Number, default: 0 },
    width: { type: String, default: '100%' },
    height: { type: String, default: '400px' },
    backgroundColor: { type: String, default: 'var(--greyLight-1)' },
    isOverflowHidden: { type: Boolean, default: true },
    duration: { type: Number, default: 500 },
    showIndicators: { type: Boolean, default: false },
    perspective: { type: Number, default: 1200 },
    swipeThreshold: { type: Number, default: 50 },
    directionAngle: { type: Number, default: 30 }
  },
  emits: ['update:modelValue', 'change'],
  data() {
    return {
      currentIndex: this.modelValue,
      // 触摸状态
      startX: 0,
      startY: 0,
      curX: 0,
      curY: 0,
      touching: false,
      isHorizontal: false,
      dragOffset: 0, // 拖拽偏移量(px)，正值=向右拖
      animating: false,
      size: 0,       // 容器宽度
      viewHeight: 0  // 容器高度
    }
  },
  computed: {
    cubeStyle() {
      return {
        transitionDuration: this.touching ? '0s' : this.duration + 'ms',
        transform: this.cubeTransform
      }
    },
    // cube 整体旋转角度
    // 当前页朝前 = cube 绕 Y 轴旋转 -currentIndex*90
    // 拖拽时额外加上 dragOffset 对应的角度
    cubeTransform() {
      let angle = -this.currentIndex * 90
      if (this.isHorizontal && this.size) {
        angle += (this.dragOffset / this.size) * 90
      }
      return `rotateY(${angle}deg)`
    },
    // 反向缩放比例：抵消 3D 透视放大，使 face 内容不会超出容器被 overflow 裁剪
    // 推导：视觉尺寸 = W * scale * perspective / (perspective - half*scale) = W
    // 解得 scale = perspective / (perspective + half)
    faceScale() {
      if (!this.size) return 1
      const half = this.size / 2
      return this.perspective / (this.perspective + half)
    }
  },
  watch: {
    modelValue(val) {
      if (val !== this.currentIndex) this.slideTo(val)
    },
    currentIndex(val) {
      this.$emit('update:modelValue', val)
      this.$emit('change', val)
    }
  },
  mounted() {
    this.$nextTick(this.measure)
    setTimeout(() => { if (!this.size) this.measure() }, 200)
  },
  methods: {
    measure() {
      uni.createSelectorQuery().in(this)
        .select('.asc__stage')
        .boundingClientRect((r) => {
          if (r) {
            this.size = r.width
            this.viewHeight = r.height
          }
        })
        .exec()
    },

    // 每个 slide 固定在立方体的某个面上
    // scale 缩小 face 抵消透视放大，translateZ 也要乘 scale 保持面贴合
    // transform 从右往左：scale → translateZ(half*scale) → rotateY
    // 先缩小 face，再推到缩小后的立方体表面，再翻面 → 面之间无缝贴合
    faceStyle(index) {
      const half = this.size ? this.size / 2 : 0
      const angle = index * 90
      const isActive = index === this.currentIndex
      const diff = Math.abs(index - this.currentIndex)
      const scale = this.faceScale
      return {
        transform: `rotateY(${angle}deg) translateZ(${half * scale}px) scale(${scale})`,
        pointerEvents: isActive ? 'auto' : 'none',
        visibility: diff <= 2 ? 'visible' : 'hidden',
        backfaceVisibility: 'hidden',
        WebkitBackfaceVisibility: 'hidden'
      }
    },

    onTouchStart(e) {
      if (this.animating || !e.touches || !e.touches[0]) return
      const t = e.touches[0]
      this.startX = t.pageX
      this.startY = t.pageY
      this.curX = t.pageX
      this.curY = t.pageY
      this.touching = true
      this.isHorizontal = false
      this.dragOffset = 0
    },

    onTouchMove(e) {
      if (!this.touching || this.animating || !e.touches || !e.touches[0]) return
      const t = e.touches[0]
      this.curX = t.pageX
      this.curY = t.pageY
      const dx = this.curX - this.startX
      const dy = this.curY - this.startY

      // 首次移动判定方向
      if (!this.isHorizontal && (Math.abs(dx) > 8 || Math.abs(dy) > 8)) {
        const ang = (Math.atan2(Math.abs(dy), Math.abs(dx)) * 180) / Math.PI
        if (ang < this.directionAngle) {
          this.isHorizontal = true
        } else {
          // 垂直滑动 → 放弃，让内部滚动
          this.touching = false
          return
        }
      }

      if (this.isHorizontal) {
        if (e.cancelable) e.preventDefault()
        let offset = dx
        // 边界弹性
        if ((this.currentIndex === 0 && offset > 0) ||
            (this.currentIndex === this.list.length - 1 && offset < 0)) {
          offset = offset * 0.3
        }
        this.dragOffset = offset
      }
    },

    onTouchEnd() {
      if (!this.touching) return
      if (this.isHorizontal) {
        const dx = this.curX - this.startX
        if (Math.abs(dx) > this.swipeThreshold) {
          if (dx > 0) this.goPrev()
          else this.goNext()
        } else {
          this.dragOffset = 0 // 回弹
        }
      }
      this.touching = false
      this.isHorizontal = false
      this.dragOffset = 0
    },

    onFaceClick(index) {
      if (index !== this.currentIndex) this.slideTo(index)
    },

    goPrev() {
      if (this.currentIndex > 0) this.animateTo(this.currentIndex - 1)
      else this.dragOffset = 0
    },

    goNext() {
      if (this.currentIndex < this.list.length - 1) this.animateTo(this.currentIndex + 1)
      else this.dragOffset = 0
    },

    slideTo(index) {
      if (this.animating || index === this.currentIndex) return
      if (index < 0 || index >= this.list.length) return
      this.animateTo(index)
    },

    animateTo(index) {
      this.animating = true
      this.dragOffset = 0
      this.isHorizontal = false
      this.currentIndex = index
      setTimeout(() => { this.animating = false }, this.duration + 50)
    }
  }
}
</script>

<style scoped>
.asc {
  position: relative;
  /* background-color: var(--greyLight-1); */
}

/* 3D 舞台 */
.asc__stage {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
}

/* 立方体容器，整体绕 Y 轴旋转 */
.asc__cube {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition-property: transform;
  transition-timing-function: cubic-bezier(0.25, 0.46, 0.45, 0.94);
  will-change: transform;
}

/* 立方体的每个面 */
.asc__face {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  transform-style: preserve-3d;
}

.asc__face-default {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 48px;
  color: #fff;
  background: #1989fa;
}

/* 指示器 */
.asc__dots {
  position: absolute;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
  z-index: 10;
}

.asc__dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.4);
  transition: all 0.3s;
}

.asc__dot--active {
  width: 24px;
  border-radius: 4px;
  background: #fff;
}
</style>
