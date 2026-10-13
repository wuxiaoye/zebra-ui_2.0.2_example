<template>
  <DemoPage title="NoticeBar">
    <view class="demo-notice-bar">
        
        <view class="py-10 px-20" style="color: var(--greyDark);">基础用法</view>
        <view class="pt-10 pb-20 px-20">
            <z-notice-bar
              wrapable
              text="【多行展示】zebra-swiper是基于uniapp开发的一款移动端轮播组件。"
            />
        </view>
        
      <demo-block title="滚动播放">
        <z-notice-bar
            left-icon="sound"
          scrollable
          text="【开启滚动】zebra-swiper是基于uniapp开发的一款移动端轮播组件。"
        />
        
        <view class="w-100 h-20"></view>
        <z-notice-bar
          :scrollable="false"
          text="【关闭滚动】zebra-swiper是基于uniapp开发的一款移动端轮播组件。"
        />
      </demo-block>

      <demo-block title="多行展示">
        <z-notice-bar
          wrapable
          :scrollable="false"
          text="zebra-swiper是基于uniapp开发的一款移动端轮播组件。zebra-swiper是基于uniapp开发的一款移动端轮播组件。"
        />
      </demo-block>

      <demo-block title="通知栏模式">
        <z-notice-bar
          mode="closeable"
          text="zebra-swiper是基于uniapp开发的一款移动端轮播组件。"
        />
        <view class="w-100 h-20"></view>
        
        <z-notice-bar
          mode="link"
          text="zebra-swiper是基于uniapp开发的一款移动端轮播组件。"
        />
      </demo-block>

      <demo-block title="自定义样式">
        <z-notice-bar
          text="zebra-swiper是基于uniapp开发的一款移动端轮播组件。"
          color="#9baacf"
          background="#E4EBF5"
          left-icon="setting"
        />
      </demo-block>

      <demo-block title="垂直滚动">
        <z-notice-bar left-icon="sound" :scrollable="false">
          <z-swipe
            vertical
            :custom-style="{ height: '80rpx', 'line-height': '80rpx' }"
            :autoplay="3000"
            :touchable="false"
            :show-indicators="false"
          >
            <z-swipe-item
              >zebra-swiper是基于uniapp开发的一款移动端轮播组件。</z-swipe-item
            >
            <z-swipe-item>一款移动端轮播组件。</z-swipe-item>
            <z-swipe-item>zebra-swiper</z-swipe-item>
          </z-swipe>
        </z-notice-bar>
      </demo-block>
    </view>
  </DemoPage>
</template>
