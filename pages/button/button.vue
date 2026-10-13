<template>
  <DemoPage title="Button">
    <view class="demo-button">
      <demo-block title="按钮类型">
        <view class="demo-button-item">
          <z-button type="primary">主要按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button type="success">成功按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button type="default">默认按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button type="warning">警告按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button type="danger">危险按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button type="text">文字按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button type="zi">紫色按钮</z-button>
        </view>
      </demo-block>
      
      <demo-block title="镂空按钮">
        <view class="demo-button-item">
          <z-button plain type="primary">主要按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button plain type="success">成功按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button plain type="default">默认按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button plain type="warning">警告按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button plain type="danger">危险按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button plain type="zi">紫色按钮</z-button>
        </view>
      </demo-block>
      
      <demo-block title="禁用">
        <view class="demo-button-item">
          <z-button disabled type="zi">主要按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button disabled type="success">成功按钮</z-button>
        </view>
      </demo-block>
      
      <demo-block title="加载">
        <view class="demo-button-item">
          <z-button loading type="primary"></z-button>
        </view>
        <view class="demo-button-item">
          <z-button loading type="primary" loading-type="spinner" />
        </view>
        <view class="demo-button-item">
          <z-button loading type="success" loading-text="加载中..." />
        </view>
        <view style="display: block;">
          <z-button :loading="test_loading"  type="success" @click="test_loading = !test_loading" >点击确定</z-button>
        </view>
      </demo-block>
      
      <demo-block title="形状">
        <view class="demo-button-item">
          <z-button square type="zi">方形按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button round type="zi">圆形按钮</z-button>
        </view>
      </demo-block>
      
      <demo-block title="图标按钮">
          <view class="demo-button-item">
            <z-button plain type="primary"  icon="plus" >主要按钮</z-button>
          </view>
          <view class="demo-button-item">
            <z-button plain type="success" icon="plus" >成功按钮</z-button>
          </view>
          <view class="demo-button-item">
            <z-button plain type="default" icon="plus" >默认按钮</z-button>
          </view>
          <view class="demo-button-item">
            <z-button plain type="warning" icon="plus" >警告按钮</z-button>
          </view>
          <view class="demo-button-item">
            <z-button plain type="danger" icon="plus" >危险按钮</z-button>
          </view>
          <view class="demo-button-item">
            <z-button plain type="zi" icon="plus" >紫色按钮</z-button>
          </view>
          
                <view class="demo-button-item">
                    <z-button type="primary" icon="plus" >主要按钮</z-button>
                  </view>
                  <view class="demo-button-item">
                    <z-button type="success" icon="plus" >成功按钮</z-button>
                  </view>
                  <view class="demo-button-item">
                    <z-button type="default" icon="plus" >默认按钮</z-button>
                  </view>
                  <view class="demo-button-item">
                    <z-button type="warning" icon="plus" >警告按钮</z-button>
                  </view>
                  <view class="demo-button-item">
                    <z-button type="danger" icon="plus" >危险按钮</z-button>
                  </view>
                  <view class="demo-button-item">
                    <z-button type="text" icon="plus" >文字按钮</z-button>
                  </view>
                  <view class="demo-button-item">
                    <z-button type="zi" icon="plus" >紫色按钮</z-button>
                  </view>
                  
                  <view class="demo-button-item">
                    <z-button plain icon-color="#3bb4f2" type="zi" icon="plus" >自定义 icon-color</z-button>
                  </view>
                  <view class="demo-button-item">
                    <z-button plain color="#3bb4f2" type="zi" icon="plus" >自定义 color</z-button>
                  </view>
          
        <view class="demo-button-item">
          <z-button
            icon="https://cdn.zebraui.com/zebra-ui/images/assets/demo-select.png"
            type="primary"
          >
            网络图标
          </z-button>
        </view>
      </demo-block>
      
      <demo-block title="尺寸">
        <view class="demo-button-item" style="display: block">
          <z-button size="large" type="primary">大号按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button size="normal" type="primary">普通按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button size="small" type="primary">小型按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button size="mini" type="primary">迷你按钮</z-button>
        </view>
      </demo-block>
      
      <demo-block title="块级按钮">
        <z-button block type="primary">块级按钮</z-button>
      </demo-block>
      
      <demo-block title="自定义按钮">
        <view class="demo-button-item">
          <z-button color="#ffaa00" >单色按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button color="#ffaa00" plain >单色按钮</z-button>
        </view>
        <view class="demo-button-item">
          <z-button color="linear-gradient(to right, #ff6034, #ee0a24)"  >
            渐变色按钮
          </z-button>
        </view>
      </demo-block>
      
      <demo-block title="动画按钮">
        <z-button type="danger">
          <z-swipe
            vertical
            class="notice-swipe"
            :autoplay="2000"
            :touchable="false"
            :show-indicators="false"
            :custom-style="{ height: '30rpx' }"
          >
            <z-swipe-item>按钮一</z-swipe-item>
            <z-swipe-item>按钮二</z-swipe-item>
          </z-swipe>
        </z-button>
      </demo-block>
    </view>
  </DemoPage>
</template>

<script setup>
    import { ref } from 'vue'
    
    let test_loading = ref(false)
</script>
<style scoped lang="scss">
.demo-button {
  &-item {
    display: inline-block;
    margin: 0 20rpx 20rpx 0;
  }
}
</style>
