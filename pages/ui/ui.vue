<template>
	<view class="container">
        
        <view style="margin: 40px 0;">
            <z-switch2 v-model="sw" ></z-switch2>
        </view>
        
		<view class="components">
			
			<view class="switch">
				<view class="switch_1">
					<view class="aye-switch" :class="{ 'checked': switch1 }" @tap="switch1 = !switch1"></view>
				</view>
				
				<view class="switch_1">
					<view class="aye-switch" :class="{ 'checked': switch2 }" @tap="switch2 = !switch2"></view>
				</view>
			</view>
			
			<view class="checkbox">
				<view class="aye-checkbox"  :class="{ 'checked': checkbox1 }" @tap="checkbox1 = !checkbox1">
						<uv-icon name="checkbox-mark" :color="checkbox1 ? '#07c160' : '#bbd0f9'" size="24" class="check-icon" />
				</view>
				<view class="aye-checkbox"  :class="{ 'checked': checkbox2 }" @tap="checkbox2 = !checkbox2">
						<uv-icon name="checkbox-mark" :color="checkbox2 ? '#07c160' : '#bbd0f9'" size="24" class="check-icon" />
				</view>
			</view>
			
			<view class="radio">
				<view class="aye-radio"  :class="{ 'checked': radio === 1 }" @tap="radio = 1">
						<view class="radio-dot"></view>
				</view>
				
				<view class="aye-radio"  :class="{ 'checked': radio === 2 }" @tap="radio = 2">
						<view class="radio-dot"></view>
				</view>
			</view>
			
			<view class="aye-btn btn__primary" ><text>Button</text></view>
			<view class="aye-btn btn__secondary"><text>Button</text></view>
            <!-- 动画版 -->
            <view class="aye-change-button background-color-zi btn-text-hui " @tap="aye_btn_active = !aye_btn_active"  :class="{ 'active': aye_btn_active}"  >
                <text class="button-content">斜向上动画</text>
            </view>
            
            <view class="aye-change-button ani-upward background-color-zi btn-text-hui " @tap="aye_btn_active = !aye_btn_active"  :class="{ 'active': aye_btn_active}"  >
                <text class="button-content">从下往上动画</text>
            </view>
            
            <view class="aye-change-color-button " @tap="aye_btn_active = !aye_btn_active"  :class="{ 'active': aye_btn_active}"  >
                <text class="button-content">渲染动画</text>
            </view>
			
			
			<!-- 社交媒体按钮组 -->
			 <view class="social-buttons">
				<view class="aye-plain-button zi" @tap="aye_btn_active = !aye_btn_active"  :class="{ 'active': aye_btn_active}" >
					<text class="aye-plain-button-icon" style="color: #007bb5;">{{ '\ue63a' }}</text>
				</view>
				<view class="aye-plain-button lv" @tap="aye_btn_active = ! aye_btn_active"  :class="{ 'active': aye_btn_active}">
					<text class="aye-plain-button-icon" style="color: #000000;">{{ '\ue63a' }}</text>
				</view>
                
               <view class="aye-plain-button add_shadow zi" @tap="aye_btn_active = !aye_btn_active"   :class="{ 'active': aye_btn_active}" >
                	<text class="aye-plain-button-icon" style="color: #007bb5;">{{ '\ue63a' }}</text>
                </view>
			</view>
            
			
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
			
			<view class="chip">
				<view class="chip__icon">
					<uv-icon name="star-fill" color="#07c160" size="26" />
				</view>
				<text class="chip-text">新提示设计</text>
				<view class="chip__close">
					<uv-icon name="close" color="#bec8e4" size="14" />
				</view>
			</view>
			
			<view class="circle">
				<view class="circle__btn" :class="{ 'shadow': isPlaying }" @tap="togglePlay">
					<uv-icon name="play-right-fill" color="#07c160" size="26" class="play" :class="{ 'visibility': !isPlaying }" />
					<uv-icon name="pause" color="#07c160" size="26" class="pause" :class="{ 'visibility': isPlaying }" />
				</view>
				<view class="circle__back-1" :class="{ 'paused': !isPlaying }"></view>
				<view class="circle__back-2" :class="{ 'paused': !isPlaying }"></view>
			</view>
			
			<view class="form">
				<input type="text" class="form__input" placeholder="Type anything..." placeholder-class="form-placeholder" />
			</view>
			
			<view class="search">
				<input type="text" class="search__input" placeholder="Search..." placeholder-class="search-placeholder" />
				<view class="search__icon">
					<uv-icon name="search" color="#9baacf" size="20" />
				</view>
			</view>
			
			<view class="segmented-control">
				<view :class="{ 'active': tab === 1 }" class="segmented-control-item" @tap="tab = 1">
					<text>Tab 1</text>
				</view>
				<view :class="{ 'active': tab === 2 }" class="segmented-control-item" @tap="tab = 2">
					<text>Tab 2</text>
				</view>
				<view :class="{ 'active': tab === 3 }" class="segmented-control-item" @tap="tab = 3">
					<text>Tab 3</text>
				</view>
				<view class="segmented-control-inset-box" :style="{ transform: 'translateX(' + tabOffset + '%)' }"></view>
			</view>
			
			<view class="icon">
				<view class="icon-btn" :class="{ 'pressed': iconHomePressed }" @touchstart="iconHomePressed = true" @touchend="iconHomePressed = false">
					<uv-icon name="home-fill" :color="iconHomePressed ? '#07c160' : '#9baacf'" size="20" />
				</view>
				<view class="icon-btn" :class="{ 'pressed': iconAccountPressed }" @touchstart="iconAccountPressed = true" @touchend="iconAccountPressed = false">
					<uv-icon name="account-fill" :color="iconAccountPressed ? '#07c160' : '#9baacf'" size="20" />
				</view>
				<view class="icon-btn" :class="{ 'pressed': iconSettingsPressed }" @touchstart="iconSettingsPressed = true" @touchend="iconSettingsPressed = false">
					<uv-icon name="setting-fill" :color="iconSettingsPressed ? '#07c160' : '#9baacf'" size="20" />
				</view>
			</view>
			
			<view class="slider">
				<view class="slider__box" @touchstart="onSliderStart" @touchmove="onSliderMove" @touchend="onSliderEnd">
					<view class="slider__btn" :style="{ left: sliderValue + '%' }"></view>
					<view class="slider__color" :style="{ width: sliderValue + '%' }"></view>
					<view class="slider__tooltip" :class="{ 'show': showTooltip }" :style="{ left: (sliderValue - 15) + '%' }">
						<text>{{ Math.round(sliderValue) }}%</text>
					</view>
				</view>
			</view>
		</view>
        <!-- 占位 -->
	</view>
        <view style="width: 100%; height: 50px;"></view>
	
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed, nextTick } from 'vue';
import {
    onLoad,
    onShow
  } from "@dcloudio/uni-app";
  // import { useGlobalStore } from '@/stores/index';
  // const globalStore = useGlobalStore();

//封装组件测试
let sw = ref(false);

// 开关状态
const switch1 = ref(false);
const switch2 = ref(true);

// 按钮点击状态
const btnPrimaryPressed = ref(false);
const btnSecondaryPressed = ref(false);

// 图标点击状态
const iconHomePressed = ref(false);
const iconAccountPressed = ref(false);
const iconSettingsPressed = ref(false);


// 社交媒体按钮点击处理
let aye_btn_active = ref(false);


// 复选框状态
const checkbox1 = ref(false);
const checkbox2 = ref(true);

// 单选框状态
const radio = ref(2);

// Tab状态
const tab = ref(1);
const tabOffset = computed(() => {
	if (tab.value === 1) return 0;
	if (tab.value === 2) return 100;
	if (tab.value === 3) return 200;
	return 0;
});

// 播放状态
const isPlaying = ref(true);
const togglePlay = () => {
	isPlaying.value = !isPlaying.value;
};

// 时钟状态
const hoursDeg = ref(0);
const minutesDeg = ref(0);
const secondsDeg = ref(0);
let clockTimer = null;

const updateClock = () => {
	const today = new Date();
	let h = (today.getHours() % 12) + today.getMinutes() / 59;
	let m = today.getMinutes();
	let s = today.getSeconds();
	
	hoursDeg.value = h * 30;
	minutesDeg.value = m * 6;
	secondsDeg.value = s * 6;
};

// 滑块状态
const sliderValue = ref(50);
const showTooltip = ref(false);
let startX = 0;
let startValue = 0;

const onSliderStart = (e) => {
	showTooltip.value = true;
	startX = e.touches[0].clientX;
	startValue = sliderValue.value;
};

const onSliderMove = (e) => {
	const touch = e.touches[0];
	const deltaX = touch.clientX - startX;
	// 假设滑块宽度大约是300px，根据实际调整
	const newValue = startValue + (deltaX / 300) * 100;
	sliderValue.value = Math.max(0, Math.min(100, newValue));
};

const onSliderEnd = () => {
	showTooltip.value = false;
};

onShow(() =>{
    console.log('onShow() - ui 页面 ')
    //隐藏原生底部导航栏
    uni.hideTabBar();
});
onMounted(() => {
	// 启动时钟
	updateClock();
	clockTimer = setInterval(updateClock, 500);
});

onUnmounted(() => {
	if (clockTimer) {
		clearInterval(clockTimer);
	}
});
</script>

<style>

@font-face {
  font-family: 'uvicon-iconfont';
  /* src: url('/static/icon/uvicons.ttf') format('truetype'); */
  src: url('/static/icon/uvicons.ttf') format('truetype');
}

/* 变量定义 */
:root {
    --zi-light: #8abdff;
    --zi: #6d5dfc;
    --zi-dark: #5b0eeb;
  --primary-light: #2fe25f;
  --primary: #07c160;
  --primary-dark: #0eb805;
  --white: #FFFFFF;
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
}

page {
  background: var(--greyLight-1);
  font-size: 16rpx;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: var(--greyLight-1);
  padding: 40rpx;
  padding-bottom: 120rpx;
}

.components {
  width: 80%;
  border-radius: 60rpx;
  box-shadow: 16rpx 16rpx 28rpx var(--greyLight-2), -4rpx -4rpx 36rpx var(--white);
  padding: 40rpx;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto;
  grid-row-gap: 40rpx;
  align-items: center;
}

/* SWITCH */
.switch {
  display: grid;
  grid-template-columns: repeat(2, min-content);
  grid-gap: 60rpx;
  justify-self: center;
}

.switch_1 {
  /* width: 120rpx; */
}

.aye-switch {
  display: flex;
  align-items: center;
  width: 120rpx;
  height: 60rpx;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  background: rgba(255, 255, 255, 0);
  position: relative;
  border-radius: 32rpx;
}

.aye-switch::after {
  content: "";
  position: absolute;
  left: 8rpx;
  width: 42rpx;
  height: 42rpx;
  border-radius: 50%;
  background: var(--greyDark);
  transition: all 0.4s ease;
}

.aye-switch::before {
  content: "";
  width: 100%;
  height: 100%;
  border-radius: inherit;
  background: linear-gradient(330deg, var(--primary-dark) 0%, var(--primary) 50%, var(--primary-light) 100%);
  opacity: 0;
  transition: all 0.4s ease;
}

.aye-switch.checked::before{
  opacity: 1;
}

.aye-switch.checked::after{
  left: 57%;
  background: var(--greyLight-1);
}

/* CHECKBOX */
.checkbox {
  display: grid;
  grid-template-columns: repeat(2, 120rpx);
  grid-gap: 60rpx;
  justify-content: center;
}


.aye-checkbox {
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10rpx;
  width: 56rpx;
  height: 56rpx;
}

.aye-checkbox .check-icon {
  transition: 0.3s ease;
}
.aye-checkbox.checked {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}

/* RADIO */
.radio {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  justify-items: center;
}

.aye-radio{
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50rpx;
  height: 50rpx;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.aye-radio.checked {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}

.aye-radio .radio-dot {
  content: "";
  width: 25rpx;
  height: 25rpx;
  background-color: var(--greyDark);
  border-radius: 50%;
  transition: 0.3s ease;
}

.aye-radio.checked .radio-dot {
  background-color: var(--primary);
}

/* BUTTONS */
.aye-btn {
  padding: 20rpx 80rpx;
  border-radius: 20rpx;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  justify-self: center;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 0.3s ease;
  font-size: 30rpx;
}

.aye-btn.btn__primary {
  background: var(--primary);
  box-shadow: inset 4rpx 4rpx 20rpx var(--primary-light), inset -4rpx -4rpx 20rpx var(--primary-dark), 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  color: var(--greyLight-1);
}

.aye-btn.btn__secondary {
  color: var(--greyDark);
}

.aye-btn:active {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}

.aye-btn.btn__primary:active {
  box-shadow: inset 4rpx 4rpx 20rpx var(--primary-dark), inset -4rpx -4rpx 20rpx var(--primary-light);
}



/* CLOCK */
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

.clock .marker__1 {
  top: 2%;
}

.clock .marker__2 {
  top: 98%;
  transform: translateY(-12rpx);
}

.clock .marker__3 {
  left: 2%;
}

.clock .marker__4 {
  left: 98%;
  transform: translateX(-12rpx);
}

/* CHIP */
.chip {
  justify-self: center;
  width: 340rpx;
  height: 80rpx;
  border-radius: 20rpx;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.chip__icon {
  width: 60rpx;
  height: 60rpx;
  border-radius: 20rpx;
  margin: 0 0 0 4rpx;
  display: flex;
  justify-content: center;
  align-items: center;
}

.chip .chip-text {
  font-size: 26rpx;
  color: var(--greyDark);
}

.chip__close {
  width: 32rpx;
  height: 32rpx;
  margin: 0 10rpx;
  display: flex;
}

/* PLAY BUTTON */
.circle {
  width: 180rpx;
  height: 100%;
  justify-self: center;
  border-radius: 20rpx;
  display: grid;
  grid-template-rows: 1fr;
  justify-items: center;
  align-items: center;
}

.circle__btn {
  grid-row: 1/2;
  grid-column: 1/2;
  width: 120rpx;
  height: 120rpx;
  display: flex;
  margin: 12rpx;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  font-size: 64rpx;
  color: var(--primary);
  z-index: 300;
  background: var(--greyLight-1);
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  position: relative;
}

.circle__btn.shadow {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}

.circle__btn .play {
  position: absolute;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.circle__btn .play.visibility {
  opacity: 1;
}

.circle__btn .pause {
  position: absolute;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.circle__btn .pause.visibility {
  opacity: 1;
}

.circle__back-1, .circle__back-2 {
  grid-row: 1/2;
  grid-column: 1/2;
  width: 120rpx;
  height: 120rpx;
  border-radius: 50%;
  filter: blur(2rpx);
  z-index: 100;
}

.circle__back-1 {
  box-shadow: 8rpx 8rpx 16rpx var(--greyLight-2), -8rpx -8rpx 16rpx var(--white);
  background: linear-gradient(to bottom right, var(--greyLight-2) 0%, var(--white) 100%);
  animation: waves 4s linear infinite;
}

.circle__back-1.paused {
  animation-play-state: paused;
}

.circle__back-2 {
  box-shadow: 8rpx 8rpx 16rpx var(--greyLight-2), -8rpx -8rpx 16rpx var(--white);
  animation: waves 4s linear 2s infinite;
}

.circle__back-2.paused {
  animation-play-state: paused;
}

/* FORM */
.form {
}

.form__input {
  width: 100%;
  height: 80rpx;
  border: none;
  border-radius: 20rpx;
  font-size: 28rpx;
  padding-left: 28rpx;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
  background: none;
  color: var(--greyDark);
}

.form-placeholder {
  color: var(--greyLight-3);
}

/* SEARCH */
.search {
  position: relative;
  display: flex;
  align-items: center;
}

.search__input {
  width: 100%;
  height: 80rpx;
  border: none;
  border-radius: 20rpx;
  font-size: 28rpx;
  padding-left: 76rpx;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
  background: none;
  color: var(--greyDark);
}

.search-placeholder {
  color: var(--greyLight-3);
}

.search__icon {
  height: 40rpx;
  position: absolute;
  padding: 0 20rpx;
  display: flex;
}

/* SEGMENTED-CONTROL */
.segmented-control {
  width: 100%;
  height: 80rpx;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  border-radius: 20rpx;
  display: flex;
  align-items: center;
  position: relative;
}

.segmented-control-item {
  width: 33.33%;
  height: 72rpx;
  font-size: 28rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  color: var(--greyDark);
  transition: all 0.5s ease;
  position: relative;
  z-index: 10;
}

.segmented-control-item.active {
  color: var(--primary);
}

.segmented-control-inset-box {
  position: absolute;
  height: 68rpx;
  width: calc(33.33% - 12rpx);
  left: 6rpx;
  border-radius: 16rpx;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
  pointer-events: none;
  transition: transform 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
  transform: translateX(0%);
}

/* ICONS */
.icon {
  display: flex;
  justify-content: space-between;
}

.icon-btn {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.2s ease;
}

.icon-btn.pressed {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}

/* RANGE-SLIDER */
.slider {
  align-self: center;
  display: flex;
  flex-direction: column;
}

.slider__box {
  width: 100%;
  height: 20rpx;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
  border-radius: 20rpx;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.slider__btn {
  width: 40rpx;
  height: 40rpx;
  border-radius: 50%;
  background: var(--white);
  position: absolute;
  box-shadow: 0px 2rpx 6rpx 0px var(--greyLight-3);
  z-index: 200;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: translateX(-50%);
}

.slider__btn::after {
  content: "";
  position: absolute;
  width: 16rpx;
  height: 16rpx;
  border-radius: 50%;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
}

.slider__color {
  height: 100%;
  width: 50%;
  position: absolute;
  left: 0;
  z-index: 100;
  border-radius: inherit;
  background: linear-gradient(-1deg, var(--primary-dark) 0%, var(--primary) 50%, var(--primary-light) 100%);
}

.slider__tooltip {
  position: absolute;
  top: -60rpx;
  height: 50rpx;
  width: 60rpx;
  border-radius: 12rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24rpx;
  color: var(--primary);
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  opacity: 0;
  transition: opacity 0.3s ease;
  transform: translateX(-50%);
}

.slider__tooltip.show {
  opacity: 1;
}

/* ANIMATIONS */
@keyframes waves {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: scale(2);
    opacity: 0;
  }
}

/* SOCIAL BUTTONS */
.social-buttons {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20rpx;
  padding: 20rpx 0;
  margin-top: 30rpx;
}

.social-button {
  width: 140rpx;
  height: 140rpx;
  border-radius: 40rpx;
  background-color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  box-shadow: 0 0 30rpx 0 rgba(0, 0, 0, 0.05);
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}


.social-icon {
  font-family: uvicon-iconfont;
  font-size: 60rpx;
  z-index: 1;
  position: relative;
  transition: color 0.35s ease;
}

.social-button::before {
  content: "";
  width: 120%;
  height: 120%;
  position: absolute;
  top: 90%;
  left: -110%;
  transform: rotate(45deg);
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}

.social-button.facebook::before {
  background-color: #3B5998;
}

.social-button.twitter::before {
  background-color: #55acee;
}

.social-button.google::before {
  background-color: #dd4b39;
}

.social-button.linkedin::before {
  background-color: #007bb5;
}

.social-button.github::before {
  background-color: #000000;
}

.social-button:active::before {
  top: -10%;
  left: -10%;
}

.social-button:active .social-icon {
  color: #fff !important;
}


/* 简洁按钮  */
.aye-plain-button {
  border-radius: 40rpx;
  padding: 40rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  box-shadow: 0 0 30rpx 0 rgba(0, 0, 0, 0.05);
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}

.aye-plain-button-icon {
  font-family: uvicon-iconfont;
  font-size: 60rpx;
  z-index: 1;
  position: relative;
  transition: color 0.35s ease;
}

.aye-plain-button::before {
  content: "";
  width: 120%;
  height: 120%;
  position: absolute;
  top: 90%;
  left: -110%;
  transform: rotate(45deg);
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}

.aye-plain-button.zi::before {
  background-color: #ff55ff;
}

.aye-plain-button.lv::before {
  background-color: #00ff00;
}

.aye-plain-button.active::before {
  top: -10%;
  left: -10%;
}

.aye-plain-button.active .aye-plain-button-icon {
  color: #fff !important;
}

.add_shadow{
      box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
}

.add_shadow_inset{
    box-shadow: inset 4rpx 4rpx 20rpx var(--primary-light), inset -4rpx -4rpx 20rpx var(--primary-dark), 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
}

/* 阴影按钮 - 动画: 从左下角往右上角*/
.aye-change-button {
  width: 300rpx;
  height: 80rpx;
  border-radius: 20rpx;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59); 
}
.aye-change-button .button-content {
    font-size: 30rpx;
    z-index: 1;
    position: relative;
    transition: color 0.35s ease;
}

.aye-change-button.btn-text-hui {
  color: var(--greyDark);
}

.aye-change-button::before {
  content: "";
  width: 100%;
  height: 100%;
  border-radius: 20rpx;
  position: absolute;
  top: 110%;
  left: -110%;
  transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}

.aye-change-button.background-color-zi::before {
  background: var(--primary);
  box-shadow: inset 4rpx 4rpx 20rpx var(--primary-light), inset -4rpx -4rpx 20rpx var(--primary-dark), 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  color: var(--greyLight-1);
}

.aye-change-button.active::before {
  top: 0%;
  left: 0%;
}

.aye-change-button.active{
  color: #fff !important;
}

/*  按钮动画-从下往上 , 改变颜色 */
.aye-change-button.ani-upward::before{
    top: 110%;
    left: 0%;
    transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);
}
.aye-change-button.ani-upward.active::before {
  top: 0%;
  left: 0%;
}

/* 按钮, 动画 : 缓慢渲染改变颜色 */
.aye-change-color-button {
  width: 300rpx;
  height: 80rpx;
  border-radius: 20rpx;
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.35s ease-in-out;
  color: var(--greyDark);
}
.aye-change-color-button .button-content {
    font-size: 30rpx;
    transition: color 0.35s ease-in-out;
}

.aye-change-color-button.active{
    background: var(--primary);
    box-shadow: inset 4rpx 4rpx 20rpx var(--primary-light), inset -4rpx -4rpx 20rpx var(--primary-dark), 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
    color: var(--greyLight-1);
}

</style>
