<template>
  <DemoPage title="Empty">
    <view class="demo-empty">
        <demo-block title="基础用法">
          <z-empty description="描述文字"  />
              
        </demo-block>
      
      <demo-block title="内置图标类型">
        <z-tabs v-model:active="active">
            <z-tab name="default" title="默认图标">
              <z-empty icon-type="default" description="数据为空 icon-type='default' " />
            </z-tab>
            
          <z-tab name="error" title="通用错误">
            <z-empty icon-type="error" description="通用错误 icon-type='error' " />
          </z-tab>
          
          <z-tab name="network" title="网络错误">
            <z-empty icon-type="network" description="网络错误 icon-type='network' " />
          </z-tab>
          
          <z-tab name="search" title="搜索提示">
            <z-empty icon-type="search" description="搜索为空 icon-type='search' " />
          </z-tab>
          
        </z-tabs>
      </demo-block>
      
      <demo-block title="自定义大小">
          <z-tabs >
              <z-tab name="default" title="图标大小">
                <z-empty size="300rpx" icon-type="default" description="icon 图标大小由 size 参数设置" />
              </z-tab>
              
            <z-tab name="img" title="图片大小">
              <z-empty image-size="300rpx" description="图片大小由 image-size 参数设置" image="https://cdn.zebraui.com/zebra-ui/error-network.png" />
            </z-tab>
            
          </z-tabs>
      </demo-block>
      
      <demo-block title="自定义图片">
        <z-empty
          image="https://cdn.zebraui.com/zebra-ui/empty-search.png"
          :image-size="80"
          description="描述文字"
        />
      </demo-block>

      <demo-block title="底部内容">
        <z-empty description="描述文字">
          <z-button
            type="primary"
            round
            :custom-style="{ width: '300rpx' }"
            class="bottom-button"
          >
            按钮
          </z-button>
        </z-empty>
      </demo-block>
    </view>
  </DemoPage>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
const active = ref('default')
</script>

<style scoped>
    
    
</style>