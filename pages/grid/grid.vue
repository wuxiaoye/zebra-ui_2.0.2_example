<template>
  <DemoPage title="Grid">
    <view class="demo-grid">
      <demo-block title="基础用法">
        <z-grid >
          <z-grid-item icon="scan" icon-color="#fff" icon-background="linear-gradient( 120deg, var(--primary), var(--primary-light) )" text="扫一扫" />
          <z-grid-item icon="instagram" icon-color="#fff" icon-background="linear-gradient( 120deg, #6d5dfc, #8abdff )" text="钱包" />
          <z-grid-item icon="gift" icon-color="#fff" icon-background="linear-gradient( 120deg, #f59e0b, #fcd34d )" text="福利" />
          <z-grid-item icon="heart" icon-color="#fff" icon-background="linear-gradient( 120deg, #ef4444, #fca5a5 )" text="公益" />
          <z-grid-item icon="block" icon-color="#fff" icon-background="linear-gradient( 120deg, #6d5dfc, #8abdff )" text="附近" />
          <z-grid-item icon="sketch" icon-color="#fff" icon-background="linear-gradient( 120deg,  #ec4899, #f9a8d4 )" text="商城" />
          <z-grid-item icon="CodeSandbox" icon-color="#fff" icon-background="linear-gradient( 120deg, #06b6d4, #67e8f9 )" text="游戏" />
          <z-grid-item icon="radarchart" icon-color="#fff" icon-background="linear-gradient( 120deg, #8b5cf6, #c4b5fd )" text="更多" />
        </z-grid>
      </demo-block>
      
      <demo-block title="自定义列数 + 显示边框">
        <z-grid :column-num="3" :border="true">
          <z-grid-item v-for="i in 6" :key="i" icon="image" text="文字" />
        </z-grid>
      </demo-block>
      
      <demo-block title="自定义内容">
        <z-grid :border="false" :column-num="3">
          <z-grid-item>
            <z-image
              mode="widthFix"
              src="https://cdn.zebraui.com/zebra-ui/images/swipe-demo/swipe1.jpg"
            />
          </z-grid-item>
          <z-grid-item>
            <z-image
              mode="widthFix"
              src="https://cdn.zebraui.com/zebra-ui/images/swipe-demo/swipe2.jpg"
            />
          </z-grid-item>
          <z-grid-item>
            <z-image
              mode="widthFix"
              src="https://cdn.zebraui.com/zebra-ui/images/swipe-demo/swipe3.jpg"
            />
          </z-grid-item>
        </z-grid>
      </demo-block>
      
      <demo-block title="正方形格子">
        <z-grid square>
          <z-grid-item v-for="i in 8" :key="i" icon="image" text="文字" />
        </z-grid>
      </demo-block>
      
      <demo-block title="格子间距">
        <z-grid :gutter="20" :border="false">
          <z-grid-item v-for="i in 8" :key="i" icon="image" text="文字" />
        </z-grid>
      </demo-block>
      
      <demo-block title="内容横排">
        <z-grid direction="horizontal" :column-num="3">
          <z-grid-item icon="image" text="文字" />
          <z-grid-item icon="image" text="文字" />
          <z-grid-item icon="image" text="文字" />
        </z-grid>
      </demo-block>
      
      <demo-block title="徽标提示">
        <z-grid :column-num="2">
          <z-grid-item icon="home" text="文字" dot />
          <z-grid-item icon="search" text="文字" badge="99+" />
        </z-grid>
      </demo-block>
    </view>
  </DemoPage>
</template>
<style lang="scss" scoped>
.demo-grid {
  color: var(--z-text-color);
}
</style>
