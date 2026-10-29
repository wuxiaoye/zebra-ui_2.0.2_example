<template>
  <view class="clock">
    <view class="hand hours" :style="{ transform: 'rotate(' + hoursDeg + 'deg)' }"></view>
    <view class="hand minutes" :style="{ transform: 'rotate(' + minutesDeg + 'deg)' }"></view>
    <view class="hand seconds" :style="{ transform: 'rotate(' + secondsDeg + 'deg)' }"></view>
    <view class="point"></view>
    <view class="marker">
      <view class="marker__1"></view>
      <view class="marker__2"></view>
      <view class="marker__3"></view>
      <view class="marker__4"></view>
    </view>
  </view>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const hoursDeg = ref(0);
const minutesDeg = ref(0);
const secondsDeg = ref(0);
let timer = null;

const updateClock = () => {
  const today = new Date();
  let h = (today.getHours() % 12) + today.getMinutes() / 59;
  let m = today.getMinutes();
  let s = today.getSeconds();
  hoursDeg.value = h * 30;
  minutesDeg.value = m * 6;
  secondsDeg.value = s * 6;
};

onMounted(() => {
  updateClock();
  timer = setInterval(updateClock, 500);
});
onUnmounted(() => clearInterval(timer));
</script>

<style scoped>
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
  --primary: #07c160;
}
.clock {
  width: 240rpx;
  height: 240rpx;
  justify-self: center;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
.clock .hand {
  position: absolute;
  transform-origin: bottom;
  bottom: 120rpx;
  border-radius: 4rpx;
  z-index: 200;
}
.clock .hours {
  width: 8rpx;
  height: 64rpx;
  background: var(--greyLight-3);
}
.clock .minutes {
  width: 8rpx;
  height: 92rpx;
  background: var(--greyDark);
}
.clock .seconds {
  width: 4rpx;
  height: 104rpx;
  background: var(--primary);
}
.clock .point {
  position: absolute;
  width: 16rpx;
  height: 16rpx;
  border-radius: 50%;
  background: var(--primary);
  z-index: 300;
}
.clock .marker {
  width: 95%;
  height: 95%;
  border-radius: 50%;
  position: relative;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}
.clock .marker__1, .clock .marker__2, .clock .marker__3, .clock .marker__4 {
  position: absolute;
  border-radius: 2rpx;
  box-shadow: inset 2rpx 2rpx 2rpx var(--greyLight-2), inset -2rpx -2rpx 2rpx var(--white);
}
.clock .marker__1, .clock .marker__2 {
  width: 4rpx;
  height: 12rpx;
  left: 112rpx;
}
.clock .marker__3, .clock .marker__4 {
  width: 12rpx;
  height: 4rpx;
  top: 112rpx;
}
.clock .marker__1 { top: 2%; }
.clock .marker__2 { top: 98%; transform: translateY(-12rpx); }
.clock .marker__3 { left: 2%; }
.clock .marker__4 { left: 98%; transform: translateX(-12rpx); }
</style>