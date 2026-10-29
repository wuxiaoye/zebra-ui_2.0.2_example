<template>
  <view class="container">
      <!-- 顶部状态栏 -->
      <view style=" height: var(--status-bar-height);"></view>
    <!-- 顶部导航 -->
    <view class="header">
      <view class="header-content">
        <view class="nav-tabs">
          <view class="nav-tab active">
            <text class="nav-tab-text">关注</text>
            <view class="nav-tab-indicator"></view>
          </view>
          <view class="nav-tab">
            <text class="nav-tab-text">发现</text>
          </view>
        </view>
        <view class="search-btn">
          <uv-icon name="search" size="18" color="#9baacf"></uv-icon>
        </view>
      </view>
    </view>

    <!-- 横向滚动分类 -->
    <view class="categories-section">
      <scroll-view scroll-x class="categories-scroll">
        <view class="categories-list">
          <view class="category-item active">
            <text class="category-text">推荐</text>
          </view>
          <view class="category-item">
            <text class="category-text">事件</text>
          </view>
          <view class="category-item">
            <text class="category-text">小说</text>
          </view>
          <view class="category-item">
            <text class="category-text">搞笑</text>
          </view>
          <view class="category-item">
            <text class="category-text">资讯</text>
          </view>
          <view class="category-item">
            <text class="category-text">美食</text>
          </view>
          <view class="category-item">
            <text class="category-text">数码</text>
          </view>
          <view class="category-item">
            <text class="category-text">情感</text>
          </view>
        </view>
      </scroll-view>
    </view>

    <!-- 双列瀑布流卡片 -->
    <view class="cards-section">
      <view class="waterfall">
        <!-- Card 1 -->
        <view class="card">
          <image src="https://hao.ayeos.cn/pic/a_6.jpg" mode="aspectFill" class="card-image" style="aspect-ratio: 4/3;"></image>
          <text class="card-title">社区周末线下聚会回顾</text>
          <view class="card-footer">
            <view class="author-info">
              <view class="avatar">
                <text class="avatar-text">林</text>
              </view>
              <text class="author-name">林小雨</text>
            </view>
            <view class="like-info">
              <uv-icon name="heart-fill" size="14" color="#07c160"></uv-icon>
              <text class="like-count">326</text>
            </view>
          </view>
        </view>

        <!-- Card 2 -->
        <view class="card">
          <image src="https://hao.ayeos.cn/pic/a_7.jpg" mode="aspectFill" class="card-image" style="aspect-ratio: 1/1;"></image>
          <text class="card-title">一个人也要好好吃饭</text>
          <view class="card-footer">
            <view class="author-info">
              <view class="avatar">
                <text class="avatar-text">张</text>
              </view>
              <text class="author-name">张大厨</text>
            </view>
            <view class="like-info">
              <uv-icon name="heart" size="14" color="#9baacf"></uv-icon>
              <text class="like-count">189</text>
            </view>
          </view>
        </view>

        <!-- Card 3 -->
        <view class="card">
          <image src="https://hao.ayeos.cn/pic/a_8.jpg" mode="aspectFill" class="card-image" style="aspect-ratio: 3/4;"></image>
          <text class="card-title">今年最值得入手的五款降噪耳机横评</text>
          <view class="card-footer">
            <view class="author-info">
              <view class="avatar">
                <text class="avatar-text">陈</text>
              </view>
              <text class="author-name">陈数码</text>
            </view>
            <view class="like-info">
              <uv-icon name="heart" size="14" color="#9baacf"></uv-icon>
              <text class="like-count">512</text>
            </view>
          </view>
        </view>

        <!-- Card 4 -->
        <view class="card">
          <image src="https://hao.ayeos.cn/pic/a_9.jpg" mode="aspectFill" class="card-image" style="aspect-ratio: 4/3;"></image>
          <text class="card-title">异地恋三年终于走到一起</text>
          <view class="card-footer">
            <view class="author-info">
              <view class="avatar">
                <text class="avatar-text">小</text>
              </view>
              <text class="author-name">小红豆</text>
            </view>
            <view class="like-info">
              <uv-icon name="heart-fill" size="14" color="#07c160"></uv-icon>
              <text class="like-count">1.2k</text>
            </view>
          </view>
        </view>

        <!-- Card 5 -->
        <view class="card">
          <image src="https://hao.ayeos.cn/pic/a_13.jpg" mode="aspectFill" class="card-image" style="aspect-ratio: 1/1;"></image>
          <text class="card-title">办公室摸鱼的一百种方式</text>
          <view class="card-footer">
            <view class="author-info">
              <view class="avatar">
                <text class="avatar-text">王</text>
              </view>
              <text class="author-name">王小乐</text>
            </view>
            <view class="like-info">
              <uv-icon name="heart" size="14" color="#9baacf"></uv-icon>
              <text class="like-count">98</text>
            </view>
          </view>
        </view>

        <!-- Card 6 -->
        <view class="card">
          <image src="https://hao.ayeos.cn/pic/a_14.jpg" mode="aspectFill" class="card-image" style="aspect-ratio: 3/4;"></image>
          <text class="card-title">新能源车主充电桩使用指南和省钱攻略</text>
          <view class="card-footer">
            <view class="author-info">
              <view class="avatar">
                <text class="avatar-text">赵</text>
              </view>
              <text class="author-name">赵车评</text>
            </view>
            <view class="like-info">
              <uv-icon name="heart-fill" size="14" color="#07c160"></uv-icon>
              <text class="like-count">743</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- 底部占位 -->
    <view style="height: 80px;"></view>
  </view>

</template>

<script setup>
import { ref } from 'vue';
import { onLoad, onShow } from "@dcloudio/uni-app";
// import { useGlobalStore } from '@/stores/index';
// const globalStore = useGlobalStore();

onShow(() => {
  // globalStore.tab_bar_current = 4;
  uni.hideTabBar();
});
</script>

<style>
/* Neumorphic Design System Variables */
:root {
  --primary-light: #2fe25f;
  --primary: #07c160;
  --primary-dark: #0eb805;
  --secondary: #6d5dfc;
  --white: #FFFFFF;
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --neu-shadow-out: 0.6rem 0.6rem 1.2rem var(--greyLight-2), -0.4rem -0.4rem 1rem var(--white);
  --neu-shadow-in: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
  --neu-shadow-sm: 0.2rem 0.2rem 0.4rem var(--greyLight-2), -0.15rem -0.15rem 0.3rem var(--white);
  --forum-background: var(--greyLight-1);
  --forum-foreground: #2d3748;
  --forum-card: var(--white);
  --forum-primary: var(--primary);
  --forum-primary-foreground: var(--white);
  --forum-muted: var(--greyLight-2);
  --forum-muted-foreground: var(--greyDark);
  --forum-border: var(--greyLight-2);
  --forum-radius-sm: 8px;
  --forum-radius-md: 12px;
  --forum-radius-lg: 16px;
  --text-xs: 0.6875rem;
  --text-sm: 0.75rem;
  --text-base: 0.875rem;
  --text-lg: 1rem;
  --text-xl: 1.125rem;
  --font-body: "Poppins", "PingFang SC", "Microsoft YaHei", sans-serif;
}

page {
  background: var(--forum-background);
  font-family: var(--font-body);
}

.container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background: var(--forum-background);
  padding-bottom: 0;
}

/* 顶部导航 */
.header {
  position: sticky;
  top: 0;
  z-index: 30;
  background: var(--forum-background);
  padding: 24rpx 32rpx 16rpx;
}

.header-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-tabs {
  display: flex;
  align-items: center;
  margin-right: 48rpx;
}

.nav-tab {
  position: relative;
  padding-bottom: 8rpx;
  margin-right: 48rpx;
}

.nav-tab-text {
  font-size: var(--text-xl);
  font-weight: 500;
  color: var(--forum-muted-foreground);
}

.nav-tab.active .nav-tab-text {
  font-weight: 600;
  color: var(--forum-foreground);
}

.nav-tab-indicator {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 40rpx;
  height: 6rpx;
  border-radius: 6rpx;
  background: linear-gradient(90deg, var(--primary-dark), var(--primary-light));
}

.search-btn {
  width: 72rpx;
  height: 72rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--forum-background);
  box-shadow: var(--neu-shadow-sm);
  border-radius: var(--forum-radius-md);
}

/* 横向滚动分类 */
.categories-section {
  padding: 16rpx 32rpx;
}

.categories-scroll {
  white-space: nowrap;
}

.categories-list {
  display: flex;
  padding: 16rpx;
}

.category-item {
  flex-shrink: 0;
  padding: 12rpx 32rpx;
  margin-right: 16rpx;
  background: var(--forum-background);
  box-shadow: var(--neu-shadow-sm);
  border-radius: var(--forum-radius-md);
}

.category-text {
  font-size: var(--text-base);
  font-weight: 500;
  color: var(--forum-muted-foreground);
  white-space: nowrap;
}

.category-item.active {
  background: linear-gradient(135deg, var(--primary-dark), var(--primary-light));
}

.category-item.active .category-text {
  color: var(--white);
}

/* 双列瀑布流卡片 */
.cards-section {
  padding: 16rpx 24rpx 0;
}

.waterfall {
  column-count: 2;
  column-gap: 24rpx;
}

.card {
  break-inside: avoid;
  margin-bottom: 24rpx;
  background: var(--forum-card);
  border-radius: 32rpx;
  padding: 16rpx;
  box-shadow: var(--neu-shadow-sm);
}

.card-image {
  width: 100%;
  border-radius: 16rpx;
  margin-bottom: 16rpx;
}

.card-title {
  display: block;
  margin-bottom: 16rpx;
  padding: 0 8rpx;
  font-size: var(--text-base);
  font-weight: 600;
  color: var(--forum-foreground);
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 8rpx 8rpx;
}

.author-info {
  display: flex;
  align-items: center;
  margin-right: 12rpx;
}

.avatar {
  width: 56rpx;
  height: 56rpx;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: var(--greyLight-1);
  margin-right: 12rpx;
}

.avatar-text {
  font-size: var(--text-xs);
  font-weight: 600;
  color: var(--forum-primary);
}

.author-name {
  font-size: var(--text-sm);
  color: var(--forum-muted-foreground);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.like-info {
  display: flex;
  align-items: center;
  margin-left: 6rpx;
}

.like-count {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
  margin-left: 6rpx;
}
</style>
