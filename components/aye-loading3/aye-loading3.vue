<template>
  <view class="circle">
    <view class="circle__btn">
        <view class="neu-spinner">
            <view class="ayeIconfont"
                :class="{
                    'aye-taiji' : props.icon == 'taiji',
                    'aye-yu' : props.icon == 'yu',
                    'aye-yun' : props.icon == 'yun'
                }"
            ></view>
        </view>
    </view>
    <view class="circle__back-1" ></view>
    <view class="circle__back-2" ></view>
  </view>
</template>

<script setup>
const props = defineProps({
    // 中间图标: 太极图 taiji / 太极鱼 yu / 太极云 yun
  icon:{
      type: String,
      default: 'yu'
  }
})
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

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

@font-face {
  font-family: "ayeIconfont"; /* Project id 5218209 */
  src: 
       url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAAVIAAsAAAAACeQAAAT7AAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHFQGYACDHAqGeIYBATYCJAMQCwoABCAFhQsHOhufCFGULU6b7Edh3LaEs1DYt+2xvuec1AofL4VTLMTD9/v9b+0j95sKFi2TSCST6O01hiTTiQlCJHsJd//XNC2rPl+V1+ePZIlH6A/yDziXjYWfU/MzloXd8O9pL5vLVMnEZCcVA5CRTo9CcPyCOP/HTJdtG+W3rclmFJnUZUkDm213bfk8ukAO/A7EDuVUZJOUm3S7aRmuzxHodWyqfsv7+Bp6r1Ilg74mHg1ejfEq17ehu3QpBmrotjZejy3ii0r6lH4APt9+Pv6bG90kNeMb3X2y8eDjV/xqcqftkH9qja4D2ydUZOxnzBPPzKEHGo/svoZeKd10Cex0t0Ski/Kvpm1tTaFM3SpMCvzHiwab+oE8z2V+xYlH4ldWSeYGmgYwlYu5O3BdzAOIr0v3PDZ0kT9fE6n3b6QyYzpoXc+qnkQWI6cJ8jBCYghyGCPXc+Tr50v3zl+rvEjN3klZyialk4tkdKS17uQC20t0AMtGo2rokiraYrvOUCyVTqyVrkdIetiSzJ2U70GbvrUcDCGl552PM6zLtBvT0CP4FmO1VYauYfxJzNUFkfUcsh/asGDdApqONNxFUymTS6UbYz3v4iVLUDWObtgUCxBPiNNCQvV9ERSlHS2RngJ0f3S8KbY1imEoENEf+SMCOiZLKYrTp2+F/BqgKAtHuWIUU1HMZtHQEqPFl23WbjWgPMqhdHBEI6G1p7X2tfQnMxEU5bhsOMuaNo0A0ELDRZfwDTuMWd//BtWnpcvkrjzz9k6HzovLnp09VenqpfOEOJ1C9L9c/T969i4VzdfkmWihLqgkXh6oDCZm/J6v+wd0bsZJF9XahQOQ8DDOEYut5GTm+Th+bv7wSfj8i6TG5DeTy7IKrr74opOm8+lBm6vyfrZxvnl2RwtUbhkvvHykwXWq3CheXujUie4lUs5IOSCgNW4fdQh4NHuq759z0hZhq61PSMqRr9V7XdYaHnhRgcEw4+QBiR6ABgIsPW7JTsLjsYEBLB5PuqHjWNzA4Ls/Cb+BeBw2OAi1QI8fHIj7/tmq+lzHTAeHLKec+pkDj1x8YuzmOuc4OWY3OObkODrLE2e6hK3WqXBOc0xJV2QpwXG7CNMoYQTsLvdQmYYbB/HCNKzTTjz6Xc3qwvl4pm1aqCfhXSAplOTYZtp4h/lGPNcDMCF3VbpxgiENLvNdUijNtfnfGuoXLi2CRETzrG2DKgqOgN0UkeEijI4Aa2k7Hv2qYVC4AMu0me8DSgC0zfmUpvN/3rk9/82tQHskb9P0HhO3s/YyOSVZ6Pi1mzsQEr/UcuFN4Z3WrEuLekxS71TjXe5+0bbT2RDsKWVQKY0WLe9Vim+6kE7oVTFaio36iyIyBl6B0LdUAyRdFkHWZwNakMfQirwBbZB3QK89F8rIdn7VEKUHm94AwqR3kAz6DrJJn9CC/IdUYlRog5wDve7Fyfn6bMbHm0y2kIfOE4ZunimdF/uJDjZLX5J/l9j80wnmLXEVjqOpGUJhRxlxeAdU974lolBxnuJ2cTNKkhwLziNyRQtEiqGuK+lLNDdPYYURmyAe5HiCQq5cRl0Cwt7JIge/5xLx3UnY2DwApG8RVgnXBpk0hjfozpR57ZnBjSr3fBYhu52RwnIptA0WIInK5lAhbxUhLqEJAqQLQzoNU15NWvKWtIXPgF58vhIpcpSo6uvUMAobHyqz+skJAAA=') format('woff2');
}

.ayeIconfont {
  font-family: "ayeIconfont" !important;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border-radius: 50%;
    font-size: 80rpx;
    color: var(--primary);
    animation: spin 1.5s linear infinite;
}

.aye-taiji:before {
  content: "\e606";
}

.aye-yun:before {
  content: "\e601";
}

.aye-yu:before {
  content: "\e603";
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
  color: var(--primary);
  z-index: 300;
  background: var(--greyLight-1);
  box-shadow: inset 2px 2px 4px var(--greyLight-2), inset -2px -2px 4px var(--white),
    6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
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
  padding: 10rpx;
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