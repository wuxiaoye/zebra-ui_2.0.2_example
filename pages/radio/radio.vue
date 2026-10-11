<template>
  <DemoPage title="Radio">
    <view class="demo-radio">
      <demo-block title="基础用法">
          <z-radio-group2 v-model="checked2" layout="vertical">
              <z-radio2 value="1" label="新设计1"></z-radio2>
              <z-radio2 value="2" label="新设计2"></z-radio2>
          </z-radio-group2>
          
          <view class="ma-30"></view>
        <z-radio-group v-model="checked">
          <z-radio name="1">单选框 1</z-radio>
          <z-radio name="2" :custom-style="{ 'margin-top': '20rpx' }"
            >单选框 2</z-radio
          >
        </z-radio-group>
      </demo-block>
      
      <demo-block title="水平排列">
          <z-radio-group2 v-model="checked2" >
              <z-radio2 value="1" label="新设计1"></z-radio2>
              <z-radio2 value="2" label="新设计2"></z-radio2>
          </z-radio-group2>
          
          <view class="ma-30"></view>
        <z-radio-group v-model="checked" direction="horizontal">
          <z-radio name="1">单选框 1</z-radio>
          <z-radio name="2">单选框 2</z-radio>
        </z-radio-group>
      </demo-block>
      
      <demo-block title="禁用状态">
          <z-radio-group2 v-model="checked2" layout="vertical" disabled>
              <z-radio2 value="1" label="新设计1"></z-radio2>
              <z-radio2 value="2" label="新设计2"></z-radio2>
          </z-radio-group2>
          
          <view class="ma-30"></view>
        <z-radio-group v-model="checked" disabled>
          <z-radio name="1">单选框 1</z-radio>
          <z-radio name="2" :custom-style="{ 'margin-top': '20rpx' }"
            >单选框 2</z-radio
          >
        </z-radio-group>
      </demo-block>
      
      <demo-block title="自定义形状">
        <z-radio-group v-model="checked" shape="square">
          <z-radio name="1">单选框 1</z-radio>
          <z-radio name="2" :custom-style="{ 'margin-top': '20rpx' }"
            >单选框 2</z-radio
          >
        </z-radio-group>

        <z-radio-group v-model="checked" shape="dot">
          <z-radio name="1" :custom-style="{ 'margin-top': '20rpx' }"
            >单选框 1</z-radio
          >
          <z-radio name="2" :custom-style="{ 'margin-top': '20rpx' }"
            >单选框 2</z-radio
          >
        </z-radio-group>
      </demo-block>
      
      <demo-block title="自定义颜色">
          <z-radio-group2 v-model="checked2" icon-active-color="#aa00ff" icon-normal-color="#aaaaff" label-color="#9a00e7">
              <z-radio2 value="1" label="新设计1" ></z-radio2>
              <z-radio2 value="2" label="新设计2"></z-radio2>
          </z-radio-group2>
          <view class="ma-30"></view>
        <z-radio-group v-model="checked" direction="horizontal">
          <z-radio name="1" checked-color="#ee0a24">单选框 1</z-radio>
          <z-radio name="2" checked-color="#ee0a24">单选框 2</z-radio>
        </z-radio-group>
      </demo-block>
      
      <demo-block title="自定义大小">
          <z-radio-group2 v-model="checked2" icon-size="70rpx" label-size="50rpx">
              <z-radio2 value="1" label="新设计1" ></z-radio2>
              <z-radio2 value="2" label="新设计2"></z-radio2>
          </z-radio-group2>
          
          <view class="ma-30"></view>
        <z-radio-group v-model="checked" direction="horizontal">
          <z-radio name="1" icon-size="48rpx">单选框 1</z-radio>
          <z-radio name="2" icon-size="48rpx">单选框 2</z-radio>
        </z-radio-group>
      </demo-block>
      
      <demo-block title="自定义图标">
        <z-radio-group v-model="checked" direction="horizontal">
          <z-radio name="1">
            单选框 1
            <template #icon>
              <image
                class="img-icon"
                :src="checked == '1' ? activeIcon : inactiveIcon"
              />
            </template>
          </z-radio>
          <z-radio name="2">
            单选框 2
            <template #icon>
              <image
                class="img-icon"
                :src="checked == '2' ? activeIcon : inactiveIcon"
              />
            </template>
          </z-radio>
        </z-radio-group>
      </demo-block>
      
      <demo-block title="左侧文本">
        <z-radio-group v-model="checked" direction="horizontal">
          <z-radio name="1" label-position="left">单选框 1</z-radio>
          <z-radio name="2" label-position="left">单选框 2</z-radio>
        </z-radio-group>
      </demo-block>
      
      <demo-block title="禁用文本点击">
        <z-radio-group v-model="checked" direction="horizontal">
          <z-radio name="1" label-disabled>单选框 1</z-radio>
          <z-radio name="2" label-disabled>单选框 2</z-radio>
        </z-radio-group>
      </demo-block>
      
      <demo-block title="其他">
          <view class="mb-30 text-size-n text-greyDark">纵向排列 + 占满一行</view>
          <z-radio-group2 v-model="checked2" layout="vertical" vertical-full >
              <z-radio2 value="1" label="新设计1"></z-radio2>
              <z-radio2 value="2" label="新设计2"></z-radio2>
          </z-radio-group2>
          <view class="ma-30"></view>
          
          <view class="my-30 text-size-n text-greyDark">纵向排列 + 占满一行 + 文字与图标换位</view>
          <z-radio-group2 v-model="checked2" layout="vertical" vertical-full reverse-align>
              <z-radio2 value="1" label="新设计1"></z-radio2>
              <z-radio2 value="2" label="新设计2"></z-radio2>
          </z-radio-group2>
          <view class="ma-30"></view>
          
          <view class="my-30 text-size-n text-greyDark">旧设计-搭配单元格组件使用</view>
        <z-radio-group v-model="checked">
          <z-cell-group>
            <z-cell title="单选框 1" clickable @click="checked = '1'">
              <template #right-icon>
                <z-radio name="1" />
              </template>
            </z-cell>
            <z-cell title="单选框 2" clickable @click="checked = '2'">
              <template #right-icon>
                <z-radio name="2" />
              </template>
            </z-cell>
          </z-cell-group>
        </z-radio-group>
      </demo-block>
    </view>
  </DemoPage>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
const checked = ref('1')
const checked2 = ref('1')
const activeIcon =
  'https://cdn.zebraui.com/zebra-ui/images/assets/demo-select.png'
const inactiveIcon =
  'https://cdn.zebraui.com/zebra-ui/images/assets/demo-noselect.png'
</script>
<style lang="scss" scoped>
.demo-radio {
  .img-icon {
    width: 40rpx;
    height: 40rpx;
  }
}
</style>
