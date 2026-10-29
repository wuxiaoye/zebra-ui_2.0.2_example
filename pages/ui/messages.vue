<template>
  <view class="container">
      <!-- 顶部状态栏 -->
      <view style=" height: var(--status-bar-height);"></view>
    <!-- Header -->
    <view class="header">
      <view class="header-inner">
        <view class="w-8"></view>
        <text class="header-title">消息</text>
        <view class="search-btn neu-flat">
          <uv-icon name="search" size="18" color="var(--forum-muted-foreground)"></uv-icon>
        </view>
      </view>
    </view>

    <!-- Category Tabs -->
    <view class="tabs-section">
      <view class="tabs-row">
        <!-- Tab 1: 赞和收藏 (active) -->
        <view class="tab-item neu-pressed" style="border-radius: var(--forum-radius-lg);">
          <text class="tab-text tab-text-active">赞和收藏</text>
          <text class="tab-badge">12</text>
        </view>
        <!-- Tab 2: 新增关注 -->
        <view class="tab-item neu-flat">
          <text class="tab-text tab-text-inactive">新增关注</text>
          <text class="tab-badge">3</text>
        </view>
        <!-- Tab 3: 评论和@ -->
        <view class="tab-item neu-flat">
          <text class="tab-text tab-text-inactive">评论和@</text>
          <text class="tab-badge">28</text>
        </view>
      </view>
    </view>

    <!-- Message List -->
    <view class="message-list">
      <!-- Message 1: 小美 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">美</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">小美</text>
            <text class="time">2分钟前</text>
          </view>
          <text class="message-desc">赞了你的帖子 "今天天气真好"</text>
        </view>
        <view class="unread-dot" style="background: var(--primary);"></view>
      </view>

      <!-- Message 2: 技术大佬 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">技</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">技术大佬</text>
            <text class="time">10分钟前</text>
          </view>
          <text class="message-desc">关注了你</text>
        </view>
        <view class="unread-dot" style="background: var(--primary);"></view>
      </view>

      <!-- Message 3: 阿花 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">花</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">阿花</text>
            <text class="time">30分钟前</text>
          </view>
          <text class="message-desc">评论了你的帖子: "写得真好！"</text>
        </view>
        <view class="unread-dot" style="background: var(--primary);"></view>
      </view>

      <!-- Message 4: 书虫 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">书</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">书虫</text>
            <text class="time">1小时前</text>
          </view>
          <text class="message-desc">@你 在 "好书推荐" 板块</text>
        </view>
        <view class="unread-dot" style="background: var(--primary);"></view>
      </view>

      <!-- Message 5: 小明 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">明</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">小明</text>
            <text class="time">2小时前</text>
          </view>
          <text class="message-desc">收藏了你的帖子 "周末美食分享"</text>
        </view>
        <view class="unread-dot" style="background: var(--primary);"></view>
      </view>

      <!-- Message 6: 旅行家 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">旅</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">旅行家</text>
            <text class="time">3小时前</text>
          </view>
          <text class="message-desc">评论了: "这个景点我也去过"</text>
        </view>
        <view class="unread-dot" style="background: var(--primary);"></view>
      </view>

      <!-- Message 7: 设计师 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">设</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">设计师</text>
            <text class="time">昨天</text>
          </view>
          <text class="message-desc">关注了你</text>
        </view>
      </view>

      <!-- Message 8: 美食家 -->
      <view class="message-item neu-flat">
        <view class="avatar" style="background: var(--forum-muted);">
          <text class="avatar-text">美</text>
        </view>
        <view class="message-content">
          <view class="message-top">
            <text class="username">美食家</text>
            <text class="time">昨天</text>
          </view>
          <text class="message-desc">赞了你的评论</text>
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
  --neu-shadow-out: 0.6rem 0.6rem 1.2rem var(--greyLight-2), -0.4rem -0.4rem 1rem var(--white);
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
  padding-bottom: 140rpx;
}

/* Header */
.header {
  position: sticky;
  top: 0;
  z-index: 30;
  padding: 24rpx 32rpx 24rpx;
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
  font-size: var(--text-xl);
  font-weight: 600;
  line-height: 1.4;
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

/* Tabs */
.tabs-section {
  padding: 0 32rpx;
  margin-bottom: 32rpx;
}
.tabs-row {
  display: flex;
}
.tab-item {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20rpx 16rpx;
  margin: 0 8rpx;
}
.tab-text {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  white-space: nowrap;
}
.tab-text-active {
  color: var(--forum-foreground);
}
.tab-text-inactive {
  color: var(--forum-muted-foreground);
}
.tab-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 40rpx;
  min-width: 40rpx;
  padding: 0 12rpx;
  color: #fff;
  font-size: var(--text-xs);
  border-radius: var(--forum-radius-full);
  background: var(--primary);
  font-weight: 600;
  margin-left: 8rpx;
}

/* Message List */
.message-list {
  padding: 0 32rpx;
}
.message-item {
  display: flex;
  align-items: center;
  padding: 24rpx;
  margin-bottom: 24rpx;
}
.avatar {
  width: 64rpx;
  height: 64rpx;
  border-radius: 50%;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 24rpx;
}
.avatar-text {
  color: #fff;
  font-weight: 600;
  font-size: var(--text-sm);
}
.message-content {
  flex: 1;
  min-width: 0;
}
.message-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 4rpx;
}
.username {
  font-weight: 600;
  font-size: var(--text-base);
  color: var(--forum-foreground);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.time {
  flex-shrink: 0;
  margin-left: 16rpx;
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
}
.message-desc {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  font-size: var(--text-sm);
  color: var(--forum-muted-foreground);
}
.unread-dot {
  width: 16rpx;
  height: 16rpx;
  border-radius: 50%;
  flex-shrink: 0;
  margin-left: 16rpx;
}
</style>
