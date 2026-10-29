<template>
  <view class="container">
      <!-- 顶部状态栏 -->
      <view style=" height: var(--status-bar-height);"></view>
    <!-- Header -->
    <view class="header">
      <view class="header-inner">
        <view class="w-8"></view>
        <text class="header-title">榜单</text>
        <view class="search-btn neu-flat">
          <uv-icon name="search" size="16" color="var(--forum-muted-foreground)"></uv-icon>
        </view>
      </view>
    </view>

    <view class="content-area">
      <!-- Section: 今日热门 -->
      <view class="section">
        <view class="section-header">
          <z-icon name="fire" size="20" color="var(--forum-primary)"></z-icon>
          <text class="section-title">今日热门</text>
        </view>
        <view class="section-list">
          <!-- Hot Post 1 -->
          <view class="hot-item neu-flat">
            <view class="rank-badge rank-badge-top">
              <text class="rank-text rank-text-top">1</text>
            </view>
            <view class="hot-content">
              <text class="hot-title">新手如何快速提升帖子曝光率？运营大神分享实战经验</text>
              <view class="hot-stats">
                <view class="stat-item">
                  <uv-icon name="eye" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">12.8k</text>
                </view>
                <view class="stat-item">
                  <uv-icon name="chat" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">326</text>
                </view>
              </view>
            </view>
          </view>

          <!-- Hot Post 2 -->
          <view class="hot-item neu-flat">
            <view class="rank-badge rank-badge-top">
              <text class="rank-text rank-text-top">2</text>
            </view>
            <view class="hot-content">
              <text class="hot-title">讨论：社区新版规则大家怎么看？</text>
              <view class="hot-stats">
                <view class="stat-item">
                  <uv-icon name="eye" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">9.4k</text>
                </view>
                <view class="stat-item">
                  <uv-icon name="chat" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">218</text>
                </view>
              </view>
            </view>
          </view>

          <!-- Hot Post 3 -->
          <view class="hot-item neu-flat">
            <view class="rank-badge rank-badge-top">
              <text class="rank-text rank-text-top">3</text>
            </view>
            <view class="hot-content">
              <text class="hot-title">周末摄影大赛投稿精选展示</text>
              <view class="hot-stats">
                <view class="stat-item">
                  <uv-icon name="eye" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">7.2k</text>
                </view>
                <view class="stat-item">
                  <uv-icon name="chat" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">156</text>
                </view>
              </view>
            </view>
          </view>

          <!-- Hot Post 4 -->
          <view class="hot-item neu-flat">
            <view class="rank-badge rank-badge-grey">
              <text class="rank-text rank-text-grey">4</text>
            </view>
            <view class="hot-content">
              <text class="hot-title">技术版块：前后端分离最佳实践</text>
              <view class="hot-stats">
                <view class="stat-item">
                  <uv-icon name="eye" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">5.6k</text>
                </view>
                <view class="stat-item">
                  <uv-icon name="chat" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">97</text>
                </view>
              </view>
            </view>
          </view>

          <!-- Hot Post 5 -->
          <view class="hot-item neu-flat">
            <view class="rank-badge rank-badge-grey">
              <text class="rank-text rank-text-grey">5</text>
            </view>
            <view class="hot-content">
              <text class="hot-title">分享一个超好用的效率工具合集</text>
              <view class="hot-stats">
                <view class="stat-item">
                  <uv-icon name="eye" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">4.1k</text>
                </view>
                <view class="stat-item">
                  <uv-icon name="chat" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">64</text>
                </view>
              </view>
            </view>
          </view>
        </view>
      </view>

      <!-- Section: 本周精华 -->
      <view class="section">
        <view class="section-header">
          <uv-icon name="integral" size="20" color="var(--forum-primary)"></uv-icon>
          <text class="section-title">本周精华</text>
        </view>
        <view class="section-list">
          <!-- Featured Post 1 -->
          <view class="featured-item neu-flat">
            <view class="medal-circle">
              <uv-icon name="integral" size="16" color="var(--forum-primary-foreground)"></uv-icon>
            </view>
            <view class="featured-content">
              <text class="featured-title">深度好文：如何构建高质量的社区内容生态</text>
              <view class="featured-meta">
                <text class="author-text">作者：林小白</text>
                <view class="stat-item">
                  <uv-icon name="heart" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">2.4k</text>
                </view>
              </view>
            </view>
          </view>

          <!-- Featured Post 2 -->
          <view class="featured-item neu-flat">
            <view class="medal-circle">
              <uv-icon name="integral" size="16" color="var(--forum-primary-foreground)"></uv-icon>
            </view>
            <view class="featured-content">
              <text class="featured-title">从零开始的个人成长笔记连载（第三期）</text>
              <view class="featured-meta">
                <text class="author-text">作者：码上飞</text>
                <view class="stat-item">
                  <uv-icon name="heart" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">1.8k</text>
                </view>
              </view>
            </view>
          </view>

          <!-- Featured Post 3 -->
          <view class="featured-item neu-flat">
            <view class="medal-circle">
              <uv-icon name="integral" size="16" color="var(--forum-primary-foreground)"></uv-icon>
            </view>
            <view class="featured-content">
              <text class="featured-title">摄影入门全攻略：从器材选择到后期修图</text>
              <view class="featured-meta">
                <text class="author-text">作者：光影手记</text>
                <view class="stat-item">
                  <uv-icon name="heart" size="12" color="var(--forum-muted-foreground)"></uv-icon>
                  <text class="stat-text">1.5k</text>
                </view>
              </view>
            </view>
          </view>
        </view>
      </view>

      <!-- Section: 热门圈子 -->
      <view class="section">
        <view class="section-header">
          <uv-icon name="account" size="20" color="var(--forum-primary)"></uv-icon>
          <text class="section-title">热门圈子</text>
        </view>
        <view class="section-list">
          <!-- Circle 1: 技术交流圈 -->
          <view class="circle-item neu-flat">
            <view class="circle-icon circle-icon-green">
              <z-icon name="code" size="20" color="var(--forum-primary-foreground)"></z-icon>
            </view>
            <view class="circle-content">
              <view class="circle-top">
                <text class="circle-name">技术交流圈</text>
                <text class="circle-members">3.2万成员</text>
              </view>
              <text class="circle-desc">编程技术、架构设计、开源项目讨论</text>
            </view>
          </view>

          <!-- Circle 2: 摄影爱好者 -->
          <view class="circle-item neu-flat">
            <view class="circle-icon circle-icon-purple">
              <uv-icon name="camera" size="20" color="var(--forum-primary-foreground)"></uv-icon>
            </view>
            <view class="circle-content">
              <view class="circle-top">
                <text class="circle-name">摄影爱好者</text>
                <text class="circle-members">2.8万成员</text>
              </view>
              <text class="circle-desc">分享作品、交流技巧、器材评测</text>
            </view>
          </view>

          <!-- Circle 3: 读书会 -->
          <view class="circle-item neu-flat">
            <view class="circle-icon circle-icon-yellow">
              <z-icon name="book" size="20" color="var(--forum-primary-foreground)"></z-icon>
            </view>
            <view class="circle-content">
              <view class="circle-top">
                <text class="circle-name">读书会</text>
                <text class="circle-members">1.9万成员</text>
              </view>
              <text class="circle-desc">好书推荐、读后感、线上共读活动</text>
            </view>
          </view>

          <!-- Circle 4: 游戏天地 -->
          <view class="circle-item neu-flat">
            <view class="circle-icon circle-icon-red">
              <z-icon name="CodeSandbox" size="20" color="var(--forum-primary-foreground)"></z-icon>
            </view>
            <view class="circle-content">
              <view class="circle-top">
                <text class="circle-name">游戏天地</text>
                <text class="circle-members">1.5万成员</text>
              </view>
              <text class="circle-desc">游戏攻略、组队开黑、新游推荐</text>
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
:root {
  --primary-light: #2fe25f;
  --primary: #07c160;
  --primary-dark: #0eb805;
  --secondary-light: #8abdff;
  --secondary: #6d5dfc;
  --secondary-dark: #5b0eeb;
  --white: #FFFFFF;
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --neu-shadow-out: 0.6rem 0.6rem 1.2rem var(--greyLight-2), -0.4rem -0.4rem 0.6rem var(--white);
  --neu-shadow-in: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
  --neu-shadow-sm: 0.2rem 0.2rem 0.4rem var(--greyLight-2), -0.15rem -0.15rem 0.3rem var(--white);
  --neu-shadow-sm-in: inset 0.15rem 0.15rem 0.3rem var(--greyLight-2), inset -0.15rem -0.15rem 0.3rem var(--white);
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
  --forum-radius-full: 9999px;
  --text-xs: 0.6875rem;
  --text-sm: 0.75rem;
  --text-base: 0.875rem;
  --text-lg: 1rem;
  --text-xl: 1.125rem;
  --text-2xl: 1.25rem;
  --text-3xl: 1.5rem;
  --state-success: var(--primary);
  --state-warning: #f59e0b;
  --state-error: #ef4444;
  --state-info: var(--secondary);
  --font-body: "Poppins", "PingFang SC", "Microsoft YaHei", sans-serif;
}

.container {
  min-height: 100vh;
  background: var(--forum-background);
}

/* Header */
.header {
  position: sticky;
  top: 0;
  z-index: 30;
  padding: 24rpx 32rpx 16rpx;
  background: var(--forum-background);
}
.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.w-8 {
  width: 64rpx;
}
.header-title {
  font-family: var(--font-body);
  font-size: var(--text-2xl);
  font-weight: 600;
  line-height: 1.3;
  color: var(--forum-foreground);
}
.search-btn {
  width: 64rpx;
  height: 64rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Neumorphic classes */
.neu-flat {
  background: var(--greyLight-1);
  box-shadow: var(--neu-shadow-out);
  border-radius: var(--forum-radius-md);
}
.neu-pressed {
  background: var(--greyLight-1);
  box-shadow: var(--neu-shadow-in);
  border-radius: var(--forum-radius-md);
}

/* Content area */
.content-area {
  padding: 0 32rpx 224rpx;
}
.section {
  margin-bottom: 48rpx;
}
.section-header {
  display: flex;
  align-items: center;
  margin-bottom: 24rpx;
}
.section-header text {
  margin-left: 16rpx;
}
.section-title {
  font-family: var(--font-body);
  font-size: var(--text-xl);
  font-weight: 600;
  line-height: 1.4;
  color: var(--forum-foreground);
}
.section-list {
  display: flex;
  flex-direction: column;
}
.section-list .neu-flat {
  margin-bottom: 24rpx;
}
.section-list .neu-flat:last-child {
  margin-bottom: 0;
}

/* Hot items */
.hot-item {
  display: flex;
  align-items: center;
  padding: 24rpx;
}
.rank-badge {
  width: 56rpx;
  height: 56rpx;
  border-radius: 16rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-right: 24rpx;
}
.rank-badge-top {
  background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
}
.rank-badge-grey {
  background: var(--greyLight-2);
}
.rank-text {
  font-size: var(--text-sm);
  font-weight: 700;
}
.rank-text-top {
  color: var(--forum-primary-foreground);
}
.rank-text-grey {
  color: var(--forum-muted-foreground);
}
.hot-content {
  flex: 1;
  min-width: 0;
}
.hot-title {
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--forum-foreground);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.hot-stats {
  display: flex;
  align-items: center;
  margin-top: 8rpx;
}
.stat-item {
  display: flex;
  align-items: center;
  margin-right: 24rpx;
}
.stat-item text {
  margin-left: 4rpx;
}
.stat-text {
  color: var(--forum-muted-foreground);
  font-size: var(--text-xs);
}

/* Featured items */
.featured-item {
  display: flex;
  align-items: flex-start;
  padding: 24rpx;
}
.medal-circle {
  width: 64rpx;
  height: 64rpx;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
  margin-right: 24rpx;
}
.featured-content {
  flex: 1;
  min-width: 0;
}
.featured-title {
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--forum-foreground);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.featured-meta {
  display: flex;
  align-items: center;
  margin-top: 8rpx;
}
.author-text {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
  margin-right: 24rpx;
}

/* Circle items */
.circle-item {
  display: flex;
  align-items: center;
  padding: 24rpx;
}
.circle-icon {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-right: 24rpx;
}
.circle-icon-green {
  background: linear-gradient(145deg, var(--forum-primary) 0%, var(--primary-light) 100%);
}
.circle-icon-purple {
  background: linear-gradient(145deg, var(--secondary) 0%, var(--secondary-light) 100%);
}
.circle-icon-yellow {
  background: linear-gradient(145deg, var(--state-warning) 0%, #fbbf24 100%);
}
.circle-icon-red {
  background: linear-gradient(145deg, var(--state-error) 0%, #f87171 100%);
}
.circle-content {
  flex: 1;
  min-width: 0;
}
.circle-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.circle-name {
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--forum-foreground);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.circle-members {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
  white-space: nowrap;
  margin-left: 16rpx;
}
.circle-desc {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-top: 4rpx;
}
</style>
