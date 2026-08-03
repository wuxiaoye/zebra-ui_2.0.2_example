<template>
  <DemoPage title="Loading">
    <view class="demo-loading">
      <demo-block title="基础用法">
        <z-row gutter="20">
          <z-col span="6">
            <z-loading />
          </z-col>
          <z-col span="6">
            <z-loading type="spinner" />
          </z-col>
          <z-col span="6">
              <aye-loading :is-show-text="false" />
          </z-col>
        </z-row>
      </demo-block>
      <demo-block title="自定义颜色">
        <z-row gutter="20">
          <z-col span="6">
            <z-loading color="#0094ff" />
          </z-col>
          <z-col span="6">
            <z-loading color="#0094ff" type="spinner" />
          </z-col>
        </z-row>
      </demo-block>
      
      <demo-block title="自定义大小">
        <z-row gutter="20">
          <z-col span="6">
            <z-loading color="#1989fa" size="24" />
          </z-col>
          <z-col span="6">
            <z-loading color="#1989fa" type="spinner" size="24" />
          </z-col>
          <z-col span="6">
              <aye-loading :is-show-text="false" size="40rpx"/>
          </z-col>
        </z-row>
      </demo-block>
      
      <demo-block title="显示文字">
        <z-row gutter="20" align="center">
          <z-col span="8">
            <z-loading size="24">加载中...</z-loading>
          </z-col>
          <z-col span="6">
            <z-loading size="24" vertical>加载中...</z-loading>
          </z-col>
          <z-col span="6">
          </z-col>
        </z-row>
        <view class="my-30"></view>
            <aye-loading size="40rpx"></aye-loading>
        <view class="my-30"></view>
            <aye-loading size="40rpx">自定义文字</aye-loading>
        <view class="my-30"></view>
            <aye-loading size="40rpx" :is-vertical="true">纵向展示</aye-loading>
      </demo-block>
      
      <demo-block title="文本颜色">
        <z-row gutter="20" align="center">
          <z-col span="8">
            <z-loading size="24" color="#0094ff" >加载中...</z-loading>
          </z-col>
          <z-col span="6">
            <z-loading size="24" vertical color="#0094ff" text-color="#0094ff"
              >加载中...</z-loading
            >
          </z-col>
        </z-row>
        <view class="my-30"></view>
            <aye-loading text-color="var(--primary)" text-size="16px">自定义文字大小与颜色</aye-loading>
      </demo-block>
      
      <demo-block title="自定义图标">
        <z-row gutter="20" align="center">
          <z-col span="8">
            <z-loading size="30">
              <template #icon>
                <z-icon name="undo" size="30" />
              </template>
            </z-loading>
          </z-col>
          <z-col span="6">
            <z-loading size="30">
              <template #icon>
                <z-icon name="reloadtime" size="30" />
              </template>
            </z-loading>
          </z-col>
        </z-row>
      </demo-block>
    </view>
  </DemoPage>
</template>
