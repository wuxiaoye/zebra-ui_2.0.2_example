<template>
	<view class="container">
        <!-- 顶部状态栏 -->
        <view style=" height: var(--status-bar-height);"></view>
		<!-- Neumorphic Header -->
		<view class="neu-header header">
			<view class="header-placeholder"></view>
			<text class="forum-h4 header-title">板块</text>
			<view class="neu-search-btn search-btn">
				<uv-icon name="search" size="22" color="#9baacf" />
			</view>
		</view>

		<!-- Board List -->
		<view class="board-list">

			<!-- Board: 吹牛皮侃大山 -->
			<view class="neu-card board-card">
				<view class="neu-icon-circle icon-circle">
					<uv-icon name="chat" size="22" color="#FFFFFF" />
				</view>
				<view class="board-info">
					<view class="board-top">
						<text class="forum-h4 board-name">吹牛皮侃大山</text>
						<uv-icon name="arrow-right" size="22" color="#9baacf" />
					</view>
					<text class="forum-caption board-count">2.3k 帖子</text>
					<text class="forum-caption board-desc">畅所欲言，分享你的日常与想法</text>
				</view>
			</view>

			<!-- Board: 小说评论 -->
			<view class="neu-card board-card">
				<view class="neu-icon-circle icon-circle">
					<z-icon name="book" size="22" color="#FFFFFF" />
				</view>
				<view class="board-info">
					<view class="board-top">
						<text class="forum-h4 board-name">小说评论</text>
						<uv-icon name="arrow-right" size="22" color="#9baacf" />
					</view>
					<text class="forum-caption board-count">1.8k 帖子</text>
					<text class="forum-caption board-desc">好书共赏，交流阅读心得</text>
				</view>
			</view>

			<!-- Board: 小仙女鉴赏 -->
			<view class="neu-card board-card">
				<view class="neu-icon-circle icon-circle">
					<uv-icon name="star" size="22" color="#FFFFFF" />
				</view>
				<view class="board-info">
					<view class="board-top">
						<text class="forum-h4 board-name">小仙女鉴赏</text>
						<uv-icon name="arrow-right" size="22" color="#9baacf" />
					</view>
					<text class="forum-caption board-count">1.2k 帖子</text>
					<text class="forum-caption board-desc">发现美好，分享精彩瞬间</text>
				</view>
			</view>

			<!-- Board: 好书推荐 -->
			<view class="neu-card board-card">
				<view class="neu-icon-circle icon-circle">
					<uv-icon name="gift" size="22" color="#FFFFFF" />
				</view>
				<view class="board-info">
					<view class="board-top">
						<text class="forum-h4 board-name">好书推荐</text>
						<uv-icon name="arrow-right" size="22" color="#9baacf" />
					</view>
					<text class="forum-caption board-count">956 帖子</text>
					<text class="forum-caption board-desc">精选好书，值得一看再看</text>
				</view>
			</view>

			<!-- Board: 纯粹幻想 -->
			<view class="neu-card board-card">
				<view class="neu-icon-circle icon-circle">
					<uv-icon name="empty-favor" size="22" color="#FFFFFF" />
				</view>
				<view class="board-info">
					<view class="board-top">
						<text class="forum-h4 board-name">纯粹幻想</text>
						<uv-icon name="arrow-right" size="22" color="#9baacf" />
					</view>
					<text class="forum-caption board-count">876 帖子</text>
					<text class="forum-caption board-desc">发挥想象力，构建奇幻世界</text>
				</view>
			</view>

			<!-- Board: 游戏交流 -->
			<view class="neu-card board-card">
				<view class="neu-icon-circle icon-circle">
					<z-icon name="CodeSandbox" size="22" color="#FFFFFF" />
				</view>
				<view class="board-info">
					<view class="board-top">
						<text class="forum-h4 board-name">游戏交流</text>
						<uv-icon name="arrow-right" size="22" color="#9baacf" />
					</view>
					<text class="forum-caption board-count">1.5k 帖子</text>
					<text class="forum-caption board-desc">游戏攻略与心得分享</text>
				</view>
			</view>

			<!-- Board: 站务处理 -->
			<view class="neu-card board-card">
				<view class="neu-icon-circle icon-circle">
					<uv-icon name="coupon" size="22" color="#FFFFFF" />
				</view>
				<view class="board-info">
					<view class="board-top">
						<text class="forum-h4 board-name">站务处理</text>
						<uv-icon name="arrow-right" size="22" color="#9baacf" />
					</view>
					<text class="forum-caption board-count">234 帖子</text>
					<text class="forum-caption board-desc">论坛事务处理与反馈</text>
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
/* ========================================
   Forum APP Neumorphic Design System
   ======================================== */

:root {
  /* === Brand Colors === */
  --primary-light: #2fe25f;
  --primary: #07c160;
  --primary-dark: #0eb805;
  --secondary: #6d5dfc;
  --white: #FFFFFF;
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;

  /* === Neumorphic Shadows === */
  --neu-shadow-out: 0.6rem 0.6rem 1.2rem var(--greyLight-2), -0.4rem -0.4rem 1rem var(--white);
  --neu-shadow-in: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
  --neu-shadow-sm: 0.2rem 0.2rem 0.4rem var(--greyLight-2), -0.15rem -0.15rem 0.3rem var(--white);
  --neu-shadow-sm-in: inset 0.15rem 0.15rem 0.3rem var(--greyLight-2), inset -0.15rem -0.15rem 0.3rem var(--white);

  /* === Semantic Tokens === */
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

  /* === Typography === */
  --text-xs: 0.6875rem;
  --text-sm: 0.75rem;
  --text-base: 0.875rem;
  --text-lg: 1rem;
  --text-xl: 1.125rem;
  --font-body: "Poppins", "PingFang SC", "Microsoft YaHei", sans-serif;

  /* === Transition === */
  --transition-fast: 0.2s ease;
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
}

/* === Typography Classes === */
.forum-h4 {
  font-family: var(--font-body);
  font-size: var(--text-xl);
  font-weight: 600;
  line-height: 1.4;
  color: var(--forum-foreground);
}

.forum-caption {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  font-weight: 400;
  line-height: 1.5;
  color: var(--forum-muted-foreground);
}

/* === Header === */
.header {
  position: sticky;
  top: 0;
  z-index: 20;
  padding: 24rpx 32rpx;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-radius: 0 0 var(--forum-radius-lg) var(--forum-radius-lg);
}

.header-placeholder {
  width: 72rpx;
}

.header-title {
  color: var(--forum-foreground);
}

.neu-header {
  background: var(--greyLight-1);
  box-shadow: 4rpx 4rpx 8rpx var(--greyLight-2), -2rpx -2rpx 6rpx var(--white);
}

/* === Search Button === */
.search-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 72rpx;
  height: 72rpx;
  border-radius: var(--forum-radius-md);
}

.neu-search-btn {
  background: var(--greyLight-1);
  box-shadow: var(--neu-shadow-sm-in);
}

/* === Board List === */
.board-list {
  flex: 1;
  display: flex;
  flex-direction: column;
  padding: 32rpx;
}

/* === Board Card === */
.board-card {
  display: flex;
  align-items: center;
  padding: 32rpx;
  margin-bottom: 24rpx;
}

.board-card:last-child {
  margin-bottom: 0;
}

.neu-card {
  background: var(--forum-card);
  box-shadow: 4rpx 4rpx 8rpx var(--greyLight-2), -2rpx -2rpx 6rpx var(--white);
  border-radius: var(--forum-radius-lg);
  transition: box-shadow var(--transition-fast);
}

.neu-card:active {
  box-shadow: inset 4rpx 4rpx 8rpx var(--greyLight-2), inset -2rpx -2rpx 6rpx var(--white);
}

/* === Icon Circle === */
.icon-circle {
  flex-shrink: 0;
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 24rpx;
}

.neu-icon-circle {
  background: var(--forum-primary);
  box-shadow: 4rpx 4rpx 8rpx rgba(0,0,0,0.15), inset 2rpx 2rpx 4rpx rgba(255,255,255,0.2);
}

/* === Board Info === */
.board-info {
  flex: 1;
  min-width: 0;
}

.board-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.board-name {
  font-size: var(--text-lg);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.board-count {
  margin-top: 4rpx;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.board-desc {
  margin-top: 4rpx;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
