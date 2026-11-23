<template>
  <view class="circle">
    <view class="circle__btn"
        :class="{
            'box-shadow-white' : boxShadowType == 'white',
            'box-shadow-grey' : boxShadowType == 'grey'
        }"
    >
      <view class="neu-spinner">
        <view class="petal-spinner">
          <view
            v-for="index in 12"
            :key="index"
            :class="['petal-spinner__line', `petal-spinner__line-${index}`]"
          ></view>
        </view>
      </view>
    </view>
    <view class="circle__back-1"></view>
    <view class="circle__back-2"></view>
  </view>
</template>

<script setup>
const props = defineProps({
    // 内阴影颜色: 白色 white /灰色 grey
    //这里不设置文字，“加载中……“文字自己在外面加
  boxShadowType:{
      type: String,
      default: 'white'
  }
})
</script>

<style lang="scss" scoped>
.circle {
  width: 180rpx;
  height: 180rpx;
  justify-self: center;
  border-radius: 20rpx;
  display: grid;
  grid-template-rows: 1fr;
  justify-items: center;
  align-items: center;
  flex-shrink: 0;
}
.circle__btn {
  grid-row: 1/2;
  grid-column: 1/2;
  width: 120rpx;
  height: 120rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  color: var(--zzz-primary);
  z-index: 3;
  background: var(--zzz-greyLight-1);
  position: relative;
  padding: 10rpx;
  box-sizing: border-box;
  flex-shrink: 0;
}
.circle__btn.box-shadow-grey{
    // 灰色内阴影
    box-shadow: var(--z-loading-shadow1);
}
.circle__btn.box-shadow-white{
    // 白色内阴影
    box-shadow: var(--z-loading-shadow2);
}

.neu-spinner {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100rpx;
  height: 100rpx;
  border-radius: 50%;
  padding: 0rpx;
  flex-shrink: 0;
}

/* ========== 方案B：花瓣独立闪烁，效果更清晰 ========== */
.petal-spinner {
  position: relative;
  width: 60rpx;
  height: 60rpx;
  flex-shrink: 0;
}
.petal-spinner__line {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
.petal-spinner__line::before {
  content: '';
  display: block;
  width: 4rpx;
  height: 26%;
  margin: 0 auto;
  background-color: var(--zzz-primary);
  border-radius: 40%;
  animation: petalFade 1.9s infinite;
}

@mixin genPetal($total, $i:1) {
  @if $i <= $total {
    .petal-spinner__line-#{$i} {
      transform: rotate($i * 30deg);
      &::before{
        animation-delay: calc(1.2s / $total * ($i - 1));
      }
    }
    @include genPetal($total, $i + 1);
  }
}
@include genPetal(12);

@keyframes petalFade {
  0% {opacity: 1;}
  50% {opacity: 0.2;}
  100% {opacity: 1;}
}
/* ===================================== */

.circle__back-1,
.circle__back-2 {
  grid-row: 1/2;
  grid-column: 1/2;
  width: 120rpx;
  height: 120rpx;
  border-radius: 50%;
  filter: blur(2rpx);
  z-index: 2;
  flex-shrink: 0;
}
.circle__back-1 {
  box-shadow: var(--z-loading-shadow-circle__back-1);
  background: var(--z-loading-bg-circle__back-1);
  animation: waves 4s linear infinite;
}
// 暂停
.circle__back-1.paused {animation-play-state: paused;}
.circle__back-2 {
  box-shadow: var(--z-loading-shadow-circle__back-2);
  animation: waves 4s linear 2s infinite;
}
// 暂停
.circle__back-2.paused {animation-play-state: paused;}
@keyframes waves {
  0% {transform: scale(1); opacity: 1;}
  50% {opacity: 1;}
  100% {transform: scale(2); opacity: 0;}
}
</style>