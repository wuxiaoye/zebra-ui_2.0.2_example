<template>
  <DemoPage title="Cell">
    <view class="demo-cell">
        
        <view class="pa-20 text-size-n text-greyDark">基本用法</view>
      <demo-block :card="false">
        <z-cell-group :border="false" class="add_shadow">
          <z-cell title="单元格" value="内容" />
          <z-cell title="单元格" value="内容" label="描述信息" />
        </z-cell-group>
      </demo-block>
      
      <!-- <view class="pa-20 text-size-n text-greyDark">图标</view> -->
      <demo-block title="卡片风格-内缩">
        <z-cell-group inset>
          <z-cell title="单元格" value="内容" />
          <z-cell title="单元格" value="内容" label="描述信息" />
        </z-cell-group>
      </demo-block>
      
      <view class="pa-20 text-size-n text-greyDark">尺寸</view>
      <demo-block  :card="false">
        <z-cell-group :border="false">
          <z-cell title="单元格" value="内容" size="large" />
          <z-cell title="单元格" value="内容" label="描述信息" size="large" />
        </z-cell-group>
      </demo-block>
      
      <view class="ma-20 text-size-n text-greyDark">图标</view>
      <demo-block  :card="false">
        <z-cell-group :border="false">
          <z-cell title="用户名" value="青木" is-link icon="user" iconColor="var(--primary)"/>
          <z-cell title="我的收藏"  icon="star" is-link  iconColor="var(--secondary)"/>
          <z-cell title="隐私设置"  icon="pic-right" is-link  iconColor="#ffaa00"/>
          <z-cell title="帮助与反馈"  icon="question-circle" is-link />
        </z-cell-group>
      </demo-block>
      
        <view class="pa-20 text-size-n text-greyDark">箭头</view>
      <demo-block  :card="false">
        <z-cell-group :border="false">
          <z-cell title="单元格" is-link />
          <z-cell title="单元格" is-link value="内容" />
          <z-cell title="单元格" is-link arrow-direction="down" value="内容" />
        </z-cell-group>
      </demo-block>
      <demo-block title="分组标题">
        <z-cell-group title="分组1" :border="false" class="add_shadow" style="margin-bottom: 20px; border-radius: 10px; overflow: hidden;">
          <z-cell title="单元格" value="内容" />
        </z-cell-group>
        <z-cell-group title="分组2" :border="false" class="add_shadow_mini" style="border-radius: 10px; overflow: hidden;">
          <z-cell title="单元格" value="内容" />
        </z-cell-group>
      </demo-block>
      
              <view class="pa-20 text-size-n text-greyDark">插槽</view>
      <demo-block  :card="false">
        <z-cell value="内容" is-link>
          <!-- 使用 title 插槽来自定义标题 -->
          <template #title>
            <text class="custom-title">单元格</text>
            <z-tag type="primary">标签</z-tag>
          </template>
        </z-cell>

        <z-cell title="单元格" icon="creditcard">
          <!-- 使用 right-icon 插槽来自定义右侧图标 -->
          <template #right-icon>
            <z-icon name="search" class="search-icon" />
          </template>
        </z-cell>
      </demo-block>
      
              <view class="pa-20 text-size-n text-greyDark">垂直居中</view>
      <demo-block  :card="false">
        <z-cell center title="单元格" value="内容" label="描述信息" />
      </demo-block>
    </view>
  </DemoPage>
</template>

<script setup lang="ts"></script>

<style lang="scss" scoped>
.demo-cell {
  .custom-title {
    margin-right: 10rpx;
  }
}
</style>
