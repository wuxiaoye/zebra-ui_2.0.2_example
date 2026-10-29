<template>
	<view class="chat-page">
        <!-- 顶部状态栏 -->
        <view style=" height: var(--status-bar-height);"></view>
		<!-- Header -->
		<view class="chat-header">
			<view class="header-left">
				<view class="header-icon-btn">
					<uv-icon name="arrow-left" color="var(--greyDark)" size="18" />
				</view>
				<text class="header-title">小美</text>
			</view>
			<view class="header-icon-btn">
				<uv-icon name="more-dot-fill" color="var(--greyDark)" size="18" />
			</view>
		</view>

		<!-- Chat Messages -->
		<scroll-view scroll-y class="chat-messages" :style="{ height: messageAreaHeight + 'px' }">
			<view class="messages-inner">

				<!-- Message 1 - Left (other person) -->
				<view class="msg-row msg-left">
					<view class="avatar">
						<text class="avatar-text">美</text>
					</view>
					<view class="msg-content msg-left-content">
						<view class="bubble bubble-left">
							<text class="bubble-text bubble-text-left">你好呀，看到你发的那篇帖子了</text>
						</view>
						<text class="msg-time">10:30</text>
					</view>
				</view>

				<!-- Message 2 - Right (current user) -->
				<view class="msg-row msg-right">
					<view class="msg-content msg-right-content">
						<view class="bubble bubble-right">
							<text class="bubble-text bubble-text-right">是吗？你觉得写得怎么样？</text>
						</view>
						<text class="msg-time">10:31</text>
					</view>
				</view>

				<!-- Message 3 - Left -->
				<view class="msg-row msg-left">
					<view class="avatar">
						<text class="avatar-text">美</text>
					</view>
					<view class="msg-content msg-left-content">
						<view class="bubble bubble-left bubble-left-alt">
							<text class="bubble-text bubble-text-left">写得太好了！尤其是关于那个话题的部分</text>
						</view>
						<text class="msg-time">10:32</text>
					</view>
				</view>

				<!-- Message 4 - Right -->
				<view class="msg-row msg-right">
					<view class="msg-content msg-right-content">
						<view class="bubble bubble-right">
							<text class="bubble-text bubble-text-right">谢谢鼓励！我还在继续写后续的内容</text>
						</view>
						<text class="msg-time">10:33</text>
					</view>
				</view>

				<!-- Message 5 - Left -->
				<view class="msg-row msg-left">
					<view class="avatar">
						<text class="avatar-text">美</text>
					</view>
					<view class="msg-content msg-left-content">
						<view class="bubble bubble-left bubble-left-alt">
							<text class="bubble-text bubble-text-left">期待！写好了记得分享给我看看哦</text>
						</view>
						<text class="msg-time">10:34</text>
					</view>
				</view>

				<!-- Message 6 - Right -->
				<view class="msg-row msg-right">
					<view class="msg-content msg-right-content">
						<view class="bubble bubble-right">
							<text class="bubble-text bubble-text-right">好的，一定第一时间分享给你</text>
						</view>
						<text class="msg-time">10:35</text>
					</view>
				</view>

				<!-- Message 7 - Left -->
				<view class="msg-row msg-left">
					<view class="avatar">
						<text class="avatar-text">美</text>
					</view>
					<view class="msg-content msg-left-content">
						<view class="bubble bubble-left bubble-left-alt">
							<text class="bubble-text bubble-text-left">对了，你平时还喜欢写什么类型的文章？</text>
						</view>
						<text class="msg-time">10:36</text>
					</view>
				</view>

				<!-- Message 8 - Right -->
				<view class="msg-row msg-right">
					<view class="msg-content msg-right-content">
						<view class="bubble bubble-right">
							<text class="bubble-text bubble-text-right">主要写一些生活感悟和技术分享</text>
						</view>
						<text class="msg-time">10:37</text>
					</view>
				</view>

			</view>
		</scroll-view>

		<!-- Bottom Input Bar -->
		<view class="input-bar">
			<view class="input-bar-inner">
				<view class="input-icon-btn">
					<uv-icon name="plus" color="#9baacf" size="18" />
				</view>
				<view class="input-wrapper">
					<input type="text" placeholder="输入消息..." placeholder-class="input-placeholder" class="msg-input" />
				</view>
				<view class="input-icon-btn input-icon-btn-noshadow">
					<uv-icon name="smile" color="#9baacf" size="18" custom-prefix="aye-icon" />
				</view>
				<view class="send-btn">
					<uv-icon name="paper-plane2" color="#FFFFFF" size="18" custom-prefix="aye-icon"/>
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

const messageAreaHeight = ref(0);

onLoad(() => {
	const systemInfo = uni.getSystemInfoSync();
	const headerHeight = 56;
	const inputBarHeight = 68;
	messageAreaHeight.value = systemInfo.windowHeight - headerHeight - inputBarHeight;
});

onShow(() => {
});
</script>

<style>
/* ========================================
   Chat Page Neumorphic Design System
   ======================================== */

:root {
  /* === Brand Colors === */
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
  --neu-shadow-out: 20rpx 20rpx 40rpx var(--greyLight-2), -12rpx -12rpx 32rpx var(--white);
  --neu-shadow-in: inset 12rpx 12rpx 24rpx var(--greyLight-2), inset -12rpx -12rpx 24rpx var(--white);
  --neu-shadow-btn-primary: inset 10rpx 10rpx 20rpx rgba(0,0,0,0.1), inset -10rpx -10rpx 20rpx rgba(255,255,255,0.5), 10rpx 10rpx 20rpx var(--greyLight-2), -6rpx -6rpx 16rpx var(--white);
  --neu-shadow-btn-primary-active: inset 10rpx 10rpx 20rpx var(--primary-dark), inset -10rpx -10rpx 20rpx var(--primary-light);
  --neu-shadow-sm: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
  --neu-shadow-sm-in: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);

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
  --forum-radius-sm: 8px;
  --forum-radius-md: 12px;
  --forum-radius-lg: 16px;
  --forum-radius-full: 9999px;

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
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 12px;
  --spacing-lg: 16px;
  --spacing-xl: 24px;
  --spacing-2xl: 32px;

  /* === Surface Depth === */
  --surface-raised: var(--greyLight-1);
  --surface-sunken: var(--greyLight-1);
  --surface-card: var(--white);

  /* === Transition === */
  --transition-fast: 0.2s ease;
  --transition-normal: 0.3s ease;
  --transition-slow: 0.4s ease;
}

/* === Typography Classes === */
.forum-h1 { font-family: var(--font-display); font-size: var(--text-4xl); font-weight: 700; line-height: 1.2; color: var(--forum-foreground); }
.forum-h2 { font-family: var(--font-display); font-size: var(--text-3xl); font-weight: 600; line-height: 1.3; color: var(--forum-foreground); }
.forum-h3 { font-family: var(--font-display); font-size: var(--text-2xl); font-weight: 600; line-height: 1.3; color: var(--forum-foreground); }
.forum-h4 { font-family: var(--font-display); font-size: var(--text-xl); font-weight: 600; line-height: 1.4; color: var(--forum-foreground); }
.forum-body { font-family: var(--font-body); font-size: var(--text-base); font-weight: 400; line-height: 1.6; color: var(--forum-foreground); }
.forum-caption { font-family: var(--font-body); font-size: var(--text-sm); font-weight: 400; line-height: 1.5; color: var(--forum-muted-foreground); }

/* === Neumorphic Utility Classes === */
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
}

.neu-primary-btn:active {
  box-shadow: var(--neu-shadow-btn-primary-active);
}

.neu-secondary-btn {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-out);
  border-radius: var(--forum-radius-lg);
  color: var(--forum-muted-foreground);
}

.neu-secondary-btn:active {
  box-shadow: var(--neu-shadow-in);
}

/* === Page Layout === */
page {
  background: var(--greyLight-1);
}

.chat-page {
  display: flex;
  flex-direction: column;
  width: 100vw;
  flex-shrink: 0;
  min-height: 100vh;
  background: var(--greyLight-1);
}

/* === Header === */
.chat-header {
  position: sticky;
  top: 0;
  z-index: 30;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24rpx 32rpx;
  background: var(--greyLight-1);
  box-shadow: 0 8rpx 24rpx rgba(200,208,231,0.5), -4rpx -4rpx 12rpx rgba(255,255,255,0.8);
}

.header-left {
  display: flex;
  align-items: center;
}

.header-left .header-icon-btn {
  margin-right: 24rpx;
}

.header-title {
  font-family: var(--font-display);
  font-size: var(--text-xl);
  font-weight: 600;
  line-height: 1.4;
  color: var(--forum-foreground);
}

.header-icon-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 72rpx;
  height: 72rpx;
  border-radius: 50%;
  background: var(--greyLight-1);
  box-shadow: var(--neu-shadow-sm);
}

/* === Chat Messages === */
.chat-messages {
    box-sizing: border-box;
  flex: 1;
  padding: 32rpx;
  padding-bottom: 200rpx;
}

.messages-inner {
  display: flex;
  flex-direction: column;
}

.msg-row {
  display: flex;
  align-items: flex-start;
  margin-bottom: 32rpx;
}

.msg-left {
  justify-content: flex-start;
}

.msg-right {
  justify-content: flex-end;
}

/* Avatar */
.avatar {
  flex-shrink: 0;
  width: 72rpx;
  height: 72rpx;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--greyLight-2);
  box-shadow: var(--neu-shadow-sm);
  margin-right: 20rpx;
}

.avatar-text {
  font-size: var(--text-xs);
  font-weight: 600;
  color: var(--forum-muted-foreground);
}

/* Message Content */
.msg-content {
  max-width: 70%;
}

.msg-left-content {
  margin-left: 0;
}

.msg-right-content {
  margin-right: 0;
}

/* Bubble */
.bubble {
  padding: 20rpx 28rpx;
  border-radius: 32rpx;
}

.bubble-left {
  background: var(--greyLight-2);
  border-top-left-radius: 8rpx;
  box-shadow: 4rpx 4rpx 10rpx var(--greyLight-2), -4rpx -4rpx 8rpx rgba(255,255,255,0.6);
}

.bubble-left-alt {
  background: #dfe6ed;
}

.bubble-right {
  background: linear-gradient(135deg, var(--primary-dark) 0%, var(--primary) 50%, var(--primary-light) 100%);
  border-top-right-radius: 8rpx;
  box-shadow: 4rpx 4rpx 12rpx rgba(200,208,231,0.6), -4rpx -4rpx 10rpx rgba(255,255,255,0.3);
}

.bubble-text {
  font-family: var(--font-body);
  font-size: var(--text-base);
  font-weight: 400;
  line-height: 1.6;
}

.bubble-text-left {
  color: var(--forum-foreground);
}

.bubble-text-right {
  color: var(--white);
}

/* Message Time */
.msg-time {
  display: block;
  margin-top: 8rpx;
  text-align: right;
  font-size: var(--text-xs);
  color: var(--forum-muted-foreground);
}

/* === Bottom Input Bar === */
.input-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 30;
  padding: 16rpx 24rpx 32rpx;
  background: var(--greyLight-1);
  box-shadow: 0 -8rpx 24rpx rgba(200,208,231,0.4), 0 4rpx 8rpx rgba(255,255,255,0.8);
}

.input-bar-inner {
  display: flex;
  align-items: center;
}

.input-icon-btn {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  background: var(--greyLight-1);
  box-shadow: var(--neu-shadow-sm);
  margin-right: 20rpx;
}

.input-icon-btn-noshadow {
  background: transparent;
  box-shadow: none;
}

.input-wrapper {
  flex: 1;
  height: 80rpx;
  border-radius: 9999rpx;
  display: flex;
  align-items: center;
  padding: 0 32rpx;
  background: var(--greyLight-1);
  box-shadow: var(--neu-shadow-sm-in);
  margin-right: 20rpx;
}

.msg-input {
  flex: 1;
  background: transparent;
  font-family: var(--font-body);
  font-size: var(--text-sm);
  color: var(--forum-foreground);
}

.input-placeholder {
  color: var(--greyLight-3);
}

.send-btn {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  background: linear-gradient(145deg, var(--primary) 0%, var(--primary-light) 100%);
  box-shadow: var(--neu-shadow-sm);
}
</style>
