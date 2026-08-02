<template>
  <view class="demo-page">
    <view class="demo-header">
      <text class="demo-title">aye-swiper-cube 演示</text>
      <text class="demo-subtitle">3D 立方体翻转轮播，支持内部滚动</text>
    </view>

    <!-- 示例1: 基本用法 -->
    <view class="demo-section">
      <text class="demo-section-title">基本用法</text>
      <aye-swiper-cube
        v-model="activeIndex1"
        :list="demoList1"
        width="100%"
        height="400rpx"
        @change="onChange1"
      >
        <template #slide="{ item, index }">
          <view class="demo-slide" :style="{ backgroundColor: item.bg }">
            <text class="demo-slide-title">{{ item.title }}</text>
            <text class="demo-slide-desc">{{ item.desc }}</text>
          </view>
        </template>
      </aye-swiper-cube>
      <text class="demo-info">当前: 第 {{ activeIndex1 + 1 }} 页</text>
    </view>

    <!-- 示例2: 内容可滚动（关键测试） -->
    <view class="demo-section">
      <text class="demo-section-title">内部可滚动内容（核心特性）</text>
      <aye-swiper-cube
        v-model="activeIndex2"
        :list="scrollList"
        width="100%"
        height="600rpx"
        @change="onChange2"
      >
        <template #slide="{ item, index }">
          <scroll-view
            scroll-y
            class="demo-scroll-content"
            :style="{ backgroundColor: item.bg }"
          >
            <text class="demo-slide-title">{{ item.title }}</text>
            <text class="demo-slide-desc">手指在中间上下滑动，页面正常滚动</text>
            <view
              v-for="i in 15"
              :key="i"
              class="demo-scroll-item"
              :style="{
                backgroundColor: index % 2 === 0
                  ? `rgba(255,255,255,${0.3 - i * 0.015})`
                  : `rgba(0,0,0,${0.3 - i * 0.015})`
              }"
            >
              <text>{{ item.title }} - 第 {{ i }} 行</text>
            </view>
          </scroll-view>
        </template>
      </aye-swiper-cube>
      <text class="demo-info">当前: 第 {{ activeIndex2 + 1 }} 页（试着在中间区域上下滑动）</text>
    </view>

    <!-- 示例3: 全屏高度 -->
    <view class="demo-section">
      <text class="demo-section-title">全屏高度 + 内容滚动</text>
      <aye-swiper-cube
        v-model="activeIndex3"
        :list="fullList"
        width="100%"
        height="800rpx"
        :show-indicators="true"
        @change="onChange3"
      >
        <template #slide="{ item, index }">
          <scroll-view
            scroll-y
            class="demo-scroll-content"
            :style="{ backgroundColor: item.bg }"
          >
            <text class="demo-slide-title">{{ item.title }}</text>
            <view
              v-for="i in 20"
              :key="i"
              class="demo-scroll-item"
              :style="{
                backgroundColor: index % 2 === 0
                  ? `rgba(255,255,255,${0.25 - i * 0.01})`
                  : `rgba(0,0,0,${0.25 - i * 0.01})`
              }"
            >
              <text>{{ item.title }} - 第 {{ i }} 行</text>
            </view>
          </scroll-view>
        </template>
      </aye-swiper-cube>
    </view>
  </view>
</template>

<script>
import AyeSwiperCube from '@/components/aye-swiper-cube/index.js'

export default {
  components: { AyeSwiperCube },
  data() {
    return {
      activeIndex1: 0,
      activeIndex2: 2,
      activeIndex3: 3,
      demoList1: [
        { title: '红色', desc: '第一面', bg: '#e74c3c' },
        { title: '蓝色', desc: '第二面', bg: '#3498db' },
        { title: '绿色', desc: '第三面', bg: '#2ecc71' },
        { title: '紫色', desc: '第四面', bg: '#9b59b6' }
      ],
      scrollList: [
        { title: '基础组件', bg: '#1989fa' },
        { title: '表单组件', bg: '#07c160' },
        { title: '反馈组件', bg: '#ff976a' },
        { title: '展示组件', bg: '#9b59b6' },
        { title: '导航组件', bg: '#e74c3c' }
      ],
      fullList: [
        { title: '页面一', bg: '#2c3e50' },
        { title: '页面二', bg: '#34495e' },
        { title: '页面三', bg: '#1abc9c' },
        { title: '页面四', bg: '#16a085' }
      ]
    }
  },
  methods: {
    onChange1(index) {
      console.log('demo1 change:', index)
    },
    onChange2(index) {
      console.log('demo2 change:', index)
    },
    onChange3(index) {
      console.log('demo3 change:', index)
    }
  }
}
</script>

<style scoped>
.demo-page {
  min-height: 100vh;
  background: #f5f5f5;
  padding: 32rpx;
  box-sizing: border-box;
}

.demo-header {
  text-align: center;
  padding: 40rpx 0;
}

.demo-title {
  font-size: 40rpx;
  font-weight: bold;
  color: #333;
  display: block;
}

.demo-subtitle {
  font-size: 26rpx;
  color: #999;
  margin-top: 8rpx;
  display: block;
}

.demo-section {
  margin-bottom: 48rpx;
}

.demo-section-title {
  font-size: 30rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 20rpx;
  display: block;
}

.demo-slide {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.demo-slide-title {
  font-size: 48rpx;
  color: #fff;
  font-weight: bold;
}

.demo-slide-desc {
  font-size: 28rpx;
  color: rgba(255, 255, 255, 0.8);
  margin-top: 16rpx;
}

.demo-scroll-content {
  width: 100%;
  height: 100%;
}

.demo-scroll-item {
  padding: 24rpx 32rpx;
  margin: 8rpx 24rpx;
  border-radius: 12rpx;
}

.demo-scroll-item text {
  font-size: 28rpx;
  color: #fff;
}

.demo-info {
  font-size: 24rpx;
  color: #999;
  margin-top: 12rpx;
  text-align: center;
  display: block;
}
</style>
