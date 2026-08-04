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
:root{
    /* 变量定义 */
    --primary-light: #2fe25f;
    --primary: #07c160;
    --primary-dark: #0eb805;
    --secondary-light: #8abdff;
    --secondary: #6d5dfc;
    --secondary-dark: #5b0eeb;
    --white: #FFFFFF;
    --greyLight-1: #E4EBF5;
    --greyLight-1-dark: #d8e4f5;
    --greyLight-2: #c8d0e7;
    --greyLight-3: #bec8e4;
    --greyDark: #9baacf;
    /* 卡片外阴影样式 -超大*/
    --aye-shadow-more-big: 0.4rem 0.4rem 0.8rem var(--greyLight-2),  -0.4rem -0.4rem 0.8rem var(--white);
    /* 卡片外阴影样式 -大一些*/
    --aye-shadow-big: 6px 6px 12px var(--greyLight-2), -4px -4px 10px var(--white);
     /* 卡片外阴影样式 */
    --aye-shadow:  3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
     /* 卡片外阴影样式 - 小一些*/
    --aye-shadow-mini: 2px 2px 4px var(--greyLight-2), -1px -1px 3px var(--white);
     
     /* 内凹阴影-大一些 */
     --aye-shadow-inset-more-big: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
     /* 内凹阴影 */
    --aye-shadow-inset: inset 2px 2px 4px var(--greyLight-2), inset -2px -2px 4px var(--white);
     /* 内凹阴影-小一些 */
    --aye-shadow-inset-mini: inset 1px 1px 1px var(--greyLight-2), inset -2px -2px 4px var(--white);
}

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
  color: var(--primary);
  z-index: 3;
  background: var(--greyLight-1);
  position: relative;
  padding: 10rpx;
  box-sizing: border-box;
  flex-shrink: 0;
}
.circle__btn.box-shadow-grey{
    // 灰色内阴影
    box-shadow:
      inset 2px 2px 4px var(--greyLight-2), inset -2px -2px 4px var(--white),
      6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
}
.circle__btn.box-shadow-white{
    // 白色内阴影
    box-shadow:
        inset 6px 6px 12px var(--white), inset -6px -6px 12px var(--white),
        6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
}

.neu-spinner {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100rpx;
  height: 100rpx;
  border-radius: 50%;
  // box-shadow: inset 16rpx 16rpx 32rpx var(--greyLight-2), inset -16rpx -16rpx 32rpx var(--white);
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
  background-color: var(--primary);
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
  box-shadow: 8rpx 8rpx 16rpx var(--greyLight-2), -8rpx -8rpx 16rpx var(--white);
  background: linear-gradient(to bottom right, var(--greyLight-2) 0%, var(--white) 100%);
  animation: waves 4s linear infinite;
}
// 暂停
.circle__back-1.paused {animation-play-state: paused;}
.circle__back-2 {
  box-shadow: 8rpx 8rpx 16rpx var(--greyLight-2), -8rpx -8rpx 16rpx var(--white);
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