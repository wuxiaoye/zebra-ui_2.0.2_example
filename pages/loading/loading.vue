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
              <z-loading4 :is-show-text="false" />
          </z-col>
        </z-row>
      </demo-block>
      
      <demo-block title="新样式-loading2">
          <z-loading2 />
          <view class="my-25 text-greyDark text-size-n flex-center ">默认-白阴影</view>
          <view class="my-30"></view>
          <z-loading2 box-shadow-type="grey" />
          <view class="my-25 text-greyDark text-size-n flex-center ">灰色阴影</view>
      </demo-block>
      
      <demo-block title="新样式-loading3">
          <z-loading3 />
          <view class="my-25 text-greyDark text-size-n flex-center ">默认-双鱼</view>
          <view class="my-30"></view>
          <z-loading3  icon="yun" />
          <view class="my-25 text-greyDark text-size-n flex-center ">太极云</view>
          <z-loading3 icon="taiji" />
          <view class="my-25 text-greyDark text-size-n flex-center ">太极</view>
      </demo-block>
      
      <demo-block title="新样式-loading4">
          <view class="my-30 text-greyDark text-size-n">默认文字</view>
              <z-loading4 size="60rpx"></z-loading4>
          <view class="my-30 text-greyDark text-size-n">自定义文字</view>
              <z-loading4 size="60rpx">自定义文字</z-loading4>
          <view class="my-30 text-greyDark text-size-n">纵向展示</view>
              <z-loading4 size="60rpx" :is-vertical="true"></z-loading4>
          <view class="my-30 text-greyDark text-size-n">不展示文字</view>
              <z-loading4 :is-show-text="false" size="60rpx"/>
          <view class="my-30 text-greyDark text-size-n">自定义图标大小</view>
            <z-loading4 :is-show-text="false" size="90rpx"/>
            <view class="my-30 text-greyDark text-size-n">自定义文字</view>
            <z-loading4 text-color="var(--primary)" text-size="16px">自定义文字大小与颜色</z-loading4>
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
        </z-row>
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
