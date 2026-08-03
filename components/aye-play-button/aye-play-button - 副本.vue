<template>
  <view class="circle">
    <view class="circle__btn">
        <view class="neu-spinner">
            <view class="dot"></view>
        </view>
    </view>
    <view class="circle__back-1" ></view>
    <view class="circle__back-2" ></view>
  </view>
</template>

<script setup>

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
@font-face {
  font-family: "iconfont"; /* Project id 5208564 */
  /*  包含了两个图标: 播放、暂停。pause &#xe600;   play-right-fill &#xe62b;  */
  src: 
       url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAALAAAsAAAAABtAAAAJxAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHFQGYACDBgqBHIEhATYCJAMMCwgABCAFhGcHQRsIBhHVk1tkPwrjmFgVey4sJ6JoopBX2qOx70PwRHZfr7p6Zq1M8smIwAxQvNGBjBwxvPsBsDlXJ9SEjTBDOfvk0ReSUenS7MGHPxevgAb8bAC04ZrjIsqi6NPpRAc6ug47wtYDPAA+g+WVX82+ydcggC+5VGMar50DCJyhF8wiFovjFsgbZcY6eSzeOorF0oI3gotOtch2HDAbzD3YFt9ffuSLNxgcxVmlz6SmCVz6/DlD13jWoO9CFwLdzQAOoEAmYEFG9WeHoEgbr/jKlla6WASzaMLjiSWjukf+4xkQF6feH4BUmjPwGV+AwOeMTzAAKAAuH6EWMi78KwYJCAidvukxds2jjU/EWfs0oLD08p2JE47eSN8tzp6LKZuSJvY+H/AzMSSxlMst4fDSBLYM+TsOXeu8H3lhi+/BiOGBuz5F+JKa4tAuxuD8jGJ+gdZolxJAYEzB/3Oj68q/3n4WgM+LDqbGpgVzwPs8lsDPU0aARGtioLZN8psQQImdmDaAr5sAjxMM5cN0NQyuB8GbsBwGL+KgeBNPWS4dDn7kw8WbKviSQdNsP8KYgyLWB0hmPYEQzCkYAumFEsxNynIv4RDJF7gE8w++DJKA5fxIFtCeGLWgA/OH1aZIniax1zvOh9fclHojl5UmYGj7auGGEXmOEeUzjyIExCnAVe6G3ifInDa00i4ieeo6artJa1NQJ0Yt6MD8YbUpUkiW8vPdcT68ZpB6Z7ms1DsMbQ9QNzlCPQ+ySvnMowgBMckHuGo/9D5Bbvfb0Eq7TEjnqXNJhMrt9mr4e6IawDlbKyMqFifro2Cdvf43vM6LNLR6rxQAAAA=') format('woff2');
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: var(--primary);
  position: absolute;
  transition: all 0.3s ease;
}

.aye-icon-pause:before {
  content: "\e600";
}

.aye-icon-play-right-fill:before {
  content: "\e62b";
}
/* 稍微调整一下位置 */
.play-btn-position{
    
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
  /* font-size: 64rpx; */
  color: var(--primary);
  z-index: 300;
  background: var(--greyLight-1);
  box-shadow: inset 2px 2px 4px var(--greyLight-2), inset -2px -2px 4px var(--white),
    6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  /* box-shadow:  inset 2px 2px 4px var(--greyLight-2), inset -2px -2px 4px var(--white); */
  position: relative;
  padding: 10rpx;
  box-sizing: border-box;
}
.neu-spinner{
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    align-items: center;
  width: 100rpx;  
  height: 100rpx;
  border-radius: 50%;
  /* box-shadow: inset 6rpx 6rpx 12rpx var(--white), inset -6rpx -6rpx 12rpx var(--white); */
  box-shadow:  inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
    /* margin: 12rpx; */
  padding: 10rpx;
}
.dot{
    width: 80rpx;
    height: 80rpx;
    border-radius: 50%;
    border-width: 6rpx;
    border-style: solid;
    /* border-color: #07c160; */
    border-color: transparent  transparent #07c160 rgba(255, 255, 255, 0);
    animation: spin 1s linear infinite;
}
@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}


.circle__btn.shadow {
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
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
@keyframes waves {
  0% { transform: scale(1); opacity: 1; }
  50% { opacity: 1; }
  100% { transform: scale(2); opacity: 0; }
}
</style>