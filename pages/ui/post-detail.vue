<template>
  <view class="container">
      <!-- 顶部状态栏 -->
      <view style=" height: var(--status-bar-height);"></view>
    <!-- ========== 1. 顶部栏 ========== -->
    <view class="header">
      <view class="neu-flat top-bar">
        <!-- Left: back arrow -->
        <view class="back-btn" @tap="goBack">
          <uv-icon name="arrow-left" size="20" :color="forumForeground"></uv-icon>
        </view>
        <!-- Center: avatar + username + follow -->
        <view class="user-info">
          <view class="avatar-sm">技</view>
          <text class="username">技术大佬</text>
          <view class="follow-btn neu-primary-btn">
            <text class="follow-text">关注</text>
          </view>
        </view>
        <!-- Right: share -->
        <view class="share-btn" @tap="sharePost">
          <uv-icon name="share" size="20" :color="forumMutedForeground"></uv-icon>
        </view>
      </view>
    </view>

    <!-- ========== 2. 帖子正文 ========== -->
    <view class="content-section">
      <!-- 2a. Image gallery / carousel -->
      <view class="neu-flat gallery-container">
        <scroll-view scroll-x class="gallery-scroll" :show-scrollbar="false">
          <view class="gallery-wrapper">
            <view class="gallery-item">
              <image src="/static/forum-cover-1.jpg" mode="aspectFill" class="gallery-image"></image>
            </view>
            <view class="gallery-item">
              <image src="/static/forum-cover-2.jpg" mode="aspectFill" class="gallery-image"></image>
            </view>
            <view class="gallery-item">
              <image src="/static/forum-cover-3.jpg" mode="aspectFill" class="gallery-image"></image>
            </view>
          </view>
        </scroll-view>
        <!-- Dots indicator -->
        <view class="dots-container">
          <view class="dot dot-active"></view>
          <view class="dot dot-inactive"></view>
          <view class="dot dot-inactive"></view>
        </view>
      </view>

      <!-- 2b. Text paragraphs -->
      <view class="text-content">
        <text class="body-text">分享一个很棒的开源项目，这个项目在 GitHub 上已经获得了超过 10k 的 star，社区的活跃度也非常高。项目的主要功能是提供一个高效的后端框架，支持多种数据库和消息队列的集成。</text>
        <text class="body-text">经过我这段时间的使用体验，它的文档非常完善，API 设计也很优雅。无论是初学者还是资深开发者，都能快速上手。特别是它的插件系统，允许开发者自由扩展功能。</text>
        <text class="body-text">如果你正在寻找一个可靠的技术方案，我强烈推荐你试试这个项目。下面是一些项目的截图和功能展示。</text>
      </view>

      <!-- 2c. Inline single image -->
      <view class="inline-image-container">
        <image src="/static/forum-cover-4.jpg" mode="aspectFill" class="inline-image"></image>
      </view>

      <!-- 2d. 分享帖子 card -->
      <view class="neu-flat share-card">
        <view class="share-card-content">
          <view class="share-icon-green">
            <uv-icon name="file-text" size="16" color="#FFFFFF"></uv-icon>
          </view>
          <view class="share-card-info">
            <text class="share-label-green">分享帖子</text>
            <text class="share-title">小美</text>
            <text class="share-desc">周末美食分享</text>
            <view class="share-view-btn neu-primary-btn">
              <text class="btn-text-xs">查看</text>
            </view>
          </view>
        </view>
      </view>

      <!-- 2e. 分享文集 card -->
      <view class="neu-flat share-card mt-3">
        <view class="share-card-content">
          <view class="share-icon-purple">
            <uv-icon name="book" size="16" color="#FFFFFF"></uv-icon>
          </view>
          <view class="share-card-info">
            <text class="share-label-purple">分享文集</text>
            <text class="share-collection-title">技术文章合集</text>
            <text class="share-collection-desc">包含前端、后端、架构设计等多个方向的技术文章汇总。</text>
            <view class="share-view-btn neu-secondary-btn">
              <text class="btn-text-xs">查看</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- ========== 3. 文集信息卡片 ========== -->
    <view class="collection-section">
      <view class="neu-flat collection-card">
        <view class="collection-header">
          <uv-icon name="star-fill" size="16" :color="secondaryColor"></uv-icon>
          <text class="collection-text">本文属于文集《技术文章合集》</text>
        </view>
        <view class="collection-buttons">
          <view class="collection-btn neu-secondary-btn">
            <text class="collection-btn-text">上一篇</text>
          </view>
          <view class="collection-btn neu-secondary-btn">
            <text class="collection-btn-text">下一篇</text>
          </view>
        </view>
      </view>
    </view>

    <!-- ========== 4. 帖子底部 ========== -->
    <view class="post-footer">
      <view class="footer-info">
        <text class="footer-date">2024-01-15 14:30</text>
        <view class="footer-divider"></view>
        <view class="avatar-xs">技</view>
        <text class="footer-author">技术大佬</text>
      </view>
      <view class="section-divider"></view>
    </view>

    <!-- ========== 5. 评论区 ========== -->
    <view class="comments-section">
      <!-- Section header -->
      <text class="comments-title">评论 (28)</text>

      <!-- Comment list -->
      <view class="comments-list">
        <!-- ---- Comment 1 (读者A) ---- -->
        <view class="comment-item">
          <!-- Avatar -->
          <view class="comment-avatar">读</view>
          <!-- Bubble -->
          <view class="comment-content">
            <text class="comment-author">读者A</text>
            <view class="comment-bubble-left neu-flat">
              <text class="comment-text">写得很好，学到了很多！</text>
            </view>
            <view class="comment-meta">
              <text class="meta-time">1小时前</text>
              <view class="meta-action">
                <uv-icon name="redo" size="14" custom-prefix="aye-icon" :color="forumMutedForeground"></uv-icon>
                <text class="meta-text">回复</text>
              </view>
              <view class="meta-action">
                <uv-icon name="heart" size="14" :color="forumMutedForeground"></uv-icon>
              </view>
              <view class="meta-action">
                <uv-icon name="thumb-down" size="14" :color="forumMutedForeground"></uv-icon>
              </view>
              <text class="meta-location">北京</text>
            </view>

            <!-- ---- Reply 1 (技术大佬) ---- -->
            <view class="reply-container">
              <view class="reply-content">
                <view class="comment-bubble-right reply-bubble-green">
                  <text class="comment-text-white">谢谢支持！有什么问题可以随时交流</text>
                </view>
                <view class="reply-meta">
                  <text class="reply-author">技术大佬</text>
                  <text class="meta-time">50分钟前</text>
                  <view class="meta-action">
                    <uv-icon name="heart" size="14" :color="forumMutedForeground"></uv-icon>
                  </view>
                  <view class="meta-action">
                    <uv-icon name="thumb-down" size="14" :color="forumMutedForeground"></uv-icon>
                  </view>
                  <text class="meta-location">上海</text>
                </view>

                <!-- ---- Reply to Reply 1 (读者A) ---- -->
                <view class="reply-container">
                  <view class="reply-content">
                    <view class="comment-bubble-right reply-bubble-green">
                      <text class="comment-text-white">请问这个项目支持哪些平台？</text>
                    </view>
                    <view class="reply-meta">
                      <text class="reply-author">读者A</text>
                      <text class="meta-time">30分钟前</text>
                      <view class="meta-action">
                        <uv-icon name="heart" size="14" :color="forumMutedForeground"></uv-icon>
                      </view>
                      <view class="meta-action">
                        <uv-icon name="thumb-down" size="14" :color="forumMutedForeground"></uv-icon>
                      </view>
                      <text class="meta-location">北京</text>
                    </view>
                  </view>
                </view>
              </view>
            </view>
          </view>
        </view>

        <!-- ---- Comment 2 (码农小王) ---- -->
        <view class="comment-item">
          <!-- Avatar -->
          <view class="comment-avatar">码</view>
          <!-- Bubble -->
          <view class="comment-content">
            <text class="comment-author">码农小王</text>
            <view class="comment-bubble-left neu-flat">
              <text class="comment-text">这个项目的架构设计很棒，能分享一下设计思路吗？</text>
            </view>
            <view class="comment-meta">
              <text class="meta-time">2小时前</text>
              <view class="meta-action">
                <uv-icon name="redo" size="14" custom-prefix="aye-icon" :color="forumMutedForeground"></uv-icon>
                <text class="meta-text">回复</text>
              </view>
              <view class="meta-action">
                <uv-icon name="heart" size="14" :color="forumMutedForeground"></uv-icon>
              </view>
              <view class="meta-action">
                <uv-icon name="thumb-down" size="14" :color="forumMutedForeground"></uv-icon>
              </view>
              <text class="meta-location">深圳</text>
            </view>

            <!-- ---- Reply (技术大佬) ---- -->
            <view class="reply-container">
              <view class="reply-content">
                <view class="comment-bubble-right reply-bubble-green">
                  <text class="comment-text-white">@码农小王 我整理了一篇详细的架构分析，稍后分享</text>
                </view>
                <view class="reply-meta">
                  <text class="reply-author">技术大佬</text>
                  <text class="meta-time">1小时前</text>
                </view>
              </view>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- ========== 6. 底部输入栏 ========== -->
    <view class="input-footer">
      <view class="neu-flat input-container">
        <input type="text" placeholder="写评论..." class="comment-input" v-model="commentText" />
        <view class="send-btn neu-primary-btn" @tap="sendComment">
          <uv-icon name="paper-plane2" size="16" custom-prefix="aye-icon" color="#FFFFFF"></uv-icon>
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

const commentText = ref('');
const forumForeground = '#2d3748';
const forumMutedForeground = '#9baacf';
const secondaryColor = '#6d5dfc';

onShow(() => {
  // globalStore.tab_bar_current = 4;
  uni.hideTabBar();
});

const goBack = () => {
  uni.navigateBack();
};

const sharePost = () => {
  uni.showToast({
    title: '分享功能',
    icon: 'none'
  });
};

const sendComment = () => {
  if (!commentText.value.trim()) {
    uni.showToast({
      title: '请输入评论内容',
      icon: 'none'
    });
    return;
  }
  uni.showToast({
    title: '评论已发送',
    icon: 'success'
  });
  commentText.value = '';
};
</script>

<style>
/* ========================================
   Forum APP Neumorphic Design System
   Brand CSS — forum-app-neumorphic
   ======================================== */

:root {
  /* === Brand Colors (User-specified) === */
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

  /* === Neumorphic Shadows === */
  --neu-shadow-out: 12rpx 12rpx 24rpx var(--greyLight-2), -8rpx -8rpx 20rpx var(--white);
  --neu-shadow-in: inset 8rpx 8rpx 16rpx var(--greyLight-2), inset -8rpx -8rpx 16rpx var(--white);
  --neu-shadow-btn-primary: inset 6rpx 6rpx 12rpx rgba(0,0,0,0.1), inset -6rpx -6rpx 12rpx rgba(255,255,255,0.5), 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  --neu-shadow-btn-primary-active: inset 6rpx 6rpx 12rpx var(--primary-dark), inset -6rpx -6rpx 12rpx var(--primary-light);
  --neu-shadow-sm: 4rpx 4rpx 8rpx var(--greyLight-2), -3rpx -3rpx 6rpx var(--white);
  --neu-shadow-sm-in: inset 3rpx 3rpx 6rpx var(--greyLight-2), inset -3rpx -3rpx 6rpx var(--white);

  /* === Semantic Tokens === */
  --forum-background: var(--greyLight-1);
  --forum-foreground: #2d3748;
  --forum-card: var(--white);
  --forum-card-foreground: #2d3748;
  --forum-popover: var(--white);
  --forum-popover-foreground: #2d3748;
  --forum-primary: var(--primary);
  --forum-primary-foreground: var(--white);
  --forum-muted: var(--greyLight-2);
  --forum-muted-foreground: var(--greyDark);
  --forum-border: var(--greyLight-2);
  --forum-input: var(--greyLight-1);
  --forum-ring: var(--primary);
  --forum-radius-sm: 16rpx;
  --forum-radius-md: 24rpx;
  --forum-radius-lg: 32rpx;
  --forum-radius-full: 9999rpx;

  /* === State Colors === */
  --state-success: var(--primary);
  --state-warning: #f59e0b;
  --state-error: #ef4444;
  --state-info: var(--secondary);

  /* === Typography === */
  --font-display: "Poppins", "PingFang SC", "Microsoft YaHei", sans-serif;
  --font-body: "Poppins", "PingFang SC", "Microsoft YaHei", sans-serif;
  --font-mono: "SF Mono", "Fira Code", monospace;

  /* === Type Scale === */
  --text-xs: 22rpx;
  --text-sm: 24rpx;
  --text-base: 28rpx;
  --text-lg: 32rpx;
  --text-xl: 36rpx;
  --text-2xl: 40rpx;
  --text-3xl: 48rpx;
  --text-4xl: 64rpx;

  /* === Spacing === */
  --spacing-xs: 8rpx;
  --spacing-sm: 16rpx;
  --spacing-md: 24rpx;
  --spacing-lg: 32rpx;
  --spacing-xl: 48rpx;
  --spacing-2xl: 64rpx;

  /* === Surface Depth === */
  --surface-raised: var(--greyLight-1);
  --surface-sunken: var(--greyLight-1);
  --surface-card: var(--white);

  /* === Transition === */
  --transition-fast: 0.2s ease;
  --transition-normal: 0.3s ease;
  --transition-slow: 0.4s ease;
}

/* === Container === */
.container {
  min-height: 100vh;
  background: var(--forum-background);
  padding-bottom: 180rpx;
}

/* === Neumorphic Classes === */
.neu-flat {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-out);
  border-radius: var(--forum-radius-md);
}

.neu-pressed {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-in);
  border-radius: var(--forum-radius-md);
}

.neu-convex {
  background: linear-gradient(145deg, var(--greyLight-2) 0%, var(--white) 100%);
  box-shadow: var(--neu-shadow-out);
  border-radius: var(--forum-radius-md);
}

.neu-primary-btn {
  background: linear-gradient(330deg, var(--primary-dark) 0%, var(--primary) 50%, var(--primary-light) 100%);
  box-shadow: var(--neu-shadow-btn-primary);
  border-radius: var(--forum-radius-lg);
  color: var(--forum-primary-foreground);
  display: flex;
  align-items: center;
  justify-content: center;
}

.neu-secondary-btn {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-out);
  border-radius: var(--forum-radius-lg);
  color: var(--forum-muted-foreground);
  display: flex;
  align-items: center;
  justify-content: center;
}

/* === Header === */
.header {
  position: sticky;
  top: 0;
  z-index: 30;
  padding: 24rpx 32rpx 16rpx;
  background: var(--forum-background);
}

.top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24rpx 32rpx;
}

.back-btn {
  width: 72rpx;
  height: 72rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: var(--forum-radius-sm);
}

.user-info {
  display: flex;
  align-items: center;
  flex: 1;
  margin-left: 20rpx;
  margin-right: 20rpx;
}

.avatar-sm {
  width: 72rpx;
  height: 72rpx;
  border-radius: 50%;
  background: var(--forum-muted);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--forum-primary);
  border: 4rpx solid var(--forum-border);
  flex-shrink: 0;
}

.username {
  font-size: var(--text-lg);
  font-weight: 600;
  color: var(--forum-foreground);
  margin-left: 16rpx;
  flex: 1;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.follow-btn {
  padding: 12rpx 24rpx;
  border-radius: var(--forum-radius-full);
  flex-shrink: 0;
}

.follow-text {
  font-size: var(--text-sm);
  color: var(--forum-primary-foreground);
}

.share-btn {
  width: 72rpx;
  height: 72rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: var(--forum-radius-sm);
}

/* === Content Section === */
.content-section {
  padding: 24rpx 32rpx 0;
}

.gallery-container {
  overflow: hidden;
  border-radius: var(--forum-radius-lg);
}

.gallery-scroll {
  width: 100%;
  white-space: nowrap;
}

.gallery-wrapper {
  display: inline-flex;
}

.gallery-item {
  width: 100%;
  display: flex;
  justify-content: center;
  flex-shrink: 0;
}

.gallery-image {
  width: 100%;
  height: 440rpx;
  object-fit: cover;
}

.dots-container {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20rpx 0;
}

.dot {
  width: 16rpx;
  height: 16rpx;
  border-radius: 50%;
  margin: 0 8rpx;
}

.dot-active {
  background: var(--forum-primary);
}

.dot-inactive {
  background: var(--greyDark);
  opacity: 0.4;
}

.text-content {
  margin-top: 32rpx;
  padding: 0 8rpx;
}

.body-text {
  font-size: var(--text-base);
  line-height: 1.6;
  color: var(--forum-foreground);
  margin-bottom: 24rpx;
  display: block;
}

.inline-image-container {
  margin-top: 32rpx;
  border-radius: var(--forum-radius-lg);
  box-shadow: var(--neu-shadow-out);
  overflow: hidden;
}

.inline-image {
  width: 100%;
  height: 400rpx;
  object-fit: cover;
}

/* === Share Cards === */
.share-card {
  margin-top: 32rpx;
  padding: 28rpx;
}

.share-card-content {
  display: flex;
  align-items: flex-start;
}

.share-icon-green {
  width: 64rpx;
  height: 64rpx;
  border-radius: var(--forum-radius-sm);
  background: linear-gradient(135deg, var(--primary-dark), var(--primary-light));
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-right: 24rpx;
}

.share-icon-purple {
  width: 64rpx;
  height: 64rpx;
  border-radius: var(--forum-radius-sm);
  background: linear-gradient(135deg, var(--secondary-dark), var(--secondary-light));
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-right: 24rpx;
}

.share-card-info {
  display: flex;
  flex-direction: column;
  flex: 1;
  min-width: 0;
}

.share-label-green {
  font-size: var(--text-xs);
  color: var(--forum-primary);
  margin-bottom: 8rpx;
}

.share-label-purple {
  font-size: var(--text-xs);
  color: var(--secondary);
  margin-bottom: 8rpx;
}

.share-title {
  font-size: var(--text-xs);
  color: var(--forum-foreground);
  font-weight: 500;
  margin-bottom: 8rpx;
}

.share-desc {
  font-size: var(--text-sm);
  color: var(--forum-foreground);
  margin-bottom: 16rpx;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.share-collection-title {
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--forum-foreground);
  margin-bottom: 8rpx;
}

.share-collection-desc {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
  margin-bottom: 16rpx;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.share-view-btn {
  align-self: flex-start;
  padding: 8rpx 24rpx;
  border-radius: var(--forum-radius-full);
}

.btn-text-xs {
  font-size: var(--text-xs);
}

.mt-3 {
  margin-top: 24rpx;
}

/* === Collection Section === */
.collection-section {
  padding: 32rpx 32rpx 0;
}

.collection-card {
  padding: 32rpx;
}

.collection-header {
  display: flex;
  align-items: center;
  margin-bottom: 24rpx;
}

.collection-text {
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--forum-foreground);
  margin-left: 16rpx;
}

.collection-buttons {
  display: flex;
  align-items: center;
}

.collection-btn {
  flex: 1;
  padding: 16rpx 24rpx;
  border-radius: var(--forum-radius-md);
  margin-right: 16rpx;
}

.collection-btn:last-child {
  margin-right: 0;
}

.collection-btn-text {
  font-size: var(--text-sm);
  color: var(--forum-muted-foreground);
}

/* === Post Footer === */
.post-footer {
  padding: 32rpx 32rpx 16rpx;
}

.footer-info {
  display: flex;
  align-items: center;
  padding: 0 16rpx;
}

.footer-date {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
}

.footer-divider {
  width: 2rpx;
  height: 24rpx;
  background: var(--forum-border);
  margin: 0 16rpx;
}

.avatar-xs {
  width: 40rpx;
  height: 40rpx;
  border-radius: 50%;
  background: var(--forum-muted);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16rpx;
  font-weight: 600;
  color: var(--forum-primary);
  margin-right: 16rpx;
}

.footer-author {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
}

.section-divider {
  height: 2rpx;
  background: var(--forum-border);
  opacity: 0.5;
  margin: 32rpx 16rpx 0;
}

/* === Comments Section === */
.comments-section {
  padding: 24rpx 32rpx 48rpx;
}

.comments-title {
  font-size: var(--text-xl);
  font-weight: 600;
  color: var(--forum-foreground);
  margin-bottom: 32rpx;
  padding: 0 8rpx;
  display: block;
}

.comments-list {
  display: flex;
  flex-direction: column;
}

.comment-item {
  display: flex;
  margin-bottom: 32rpx;
}

.comment-avatar {
  width: 72rpx;
  height: 72rpx;
  border-radius: 50%;
  background: var(--forum-muted);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--forum-foreground);
  border: 4rpx solid var(--forum-border);
  flex-shrink: 0;
  margin-top: 8rpx;
  margin-right: 20rpx;
}

.comment-content {
  display: flex;
  flex-direction: column;
  flex: 1;
  min-width: 0;
}

.comment-author {
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--forum-foreground);
  margin-bottom: 12rpx;
}

.comment-bubble-left {
  padding: 28rpx;
  border-radius: 8rpx 32rpx 32rpx 32rpx;
  margin-bottom: 12rpx;
}

.comment-bubble-right {
  padding: 28rpx;
  margin-bottom: 12rpx;
}

.reply-bubble-green {
  background: linear-gradient(135deg, var(--primary-dark) 0%, var(--primary) 50%, var(--primary-light) 100%);
  border-radius: 32rpx 8rpx 32rpx 32rpx;
}

.comment-text {
  font-size: var(--text-sm);
  color: var(--forum-foreground);
  line-height: 1.5;
}

.comment-text-white {
  font-size: var(--text-sm);
  color: var(--forum-primary-foreground);
  line-height: 1.5;
}

.comment-meta {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
  margin-bottom: 24rpx;
}

.meta-time {
  margin-right: 24rpx;
}

.meta-action {
  display: flex;
  align-items: center;
  margin-right: 16rpx;
}

.meta-text {
  margin-left: 8rpx;
}

.meta-location {
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
}

.reply-container {
  display: flex;
  justify-content: flex-end;
  margin-top: 24rpx;
}

.reply-content {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  max-width: 85%;
}

.reply-meta {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
}

.reply-author {
  margin-right: 16rpx;
}

/* === Input Footer === */
.input-footer {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 40;
  padding: 16rpx 32rpx 24rpx;
  background: var(--forum-background);
}

.input-container {
  display: flex;
  align-items: center;
  padding: 20rpx 24rpx;
}

.comment-input {
  flex: 1;
  background: transparent;
  border: none;
  font-size: var(--text-sm);
  color: var(--forum-foreground);
  padding: 12rpx 24rpx;
}

.send-btn {
  width: 72rpx;
  height: 72rpx;
  border-radius: 50%;
  flex-shrink: 0;
}
</style>
