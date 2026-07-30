<template>
  <DemoPage title="Checkbox">
    <view class="demo-checkbox">
      <demo-block title="基础用法">
        <z-checkbox v-model="checked">复选框</z-checkbox>
        <view class="ma-8"></view>
        <aye-checkbox v-model="checked" label="蜂蜜"></aye-checkbox>
      </demo-block>
      
      <demo-block title="禁用状态">
        <z-checkbox v-model="checkedDisabled" disabled>复选框</z-checkbox>
        <view class="checkbox-content">
          <z-checkbox v-model="checkDisabled" disabled>复选框</z-checkbox>
        </view>
        <view class="ma-8"></view>
        <aye-checkbox v-model="checkDisabled" disabled label="被禁用的"></aye-checkbox>
      </demo-block>
      
      <demo-block title="自定义形状">
        <z-checkbox-group v-model="checkedShape" shape="square">
          <z-checkbox name="a">复选框 a</z-checkbox>
          <view class="checkbox-content">
            <z-checkbox name="b">复选框 b</z-checkbox>
          </view>
        </z-checkbox-group>
        <view class="ma-8"></view>
        <aye-checkbox v-model="checkedShape2"  label="自定义形状-方形"></aye-checkbox>
        <view class="ma-8"></view>
        <aye-checkbox v-model="checked" shape="circle" label="自定义形状-圆形"></aye-checkbox>
      </demo-block>
      
      <demo-block title="自定义颜色">
        <z-checkbox v-model="checked" checked-color="#ee0a24"
          >复选框</z-checkbox
        >
        <view class="ma-8"></view>
        <aye-checkbox v-model="checked" activeIconColor="#aa00ff" label="自定义颜色"></aye-checkbox>
      </demo-block>
      
      <demo-block title="自定义大小">
        <z-checkbox v-model="checked" icon-size="48rpx">复选框</z-checkbox>
        <view class="ma-8"></view>
        <aye-checkbox v-model="checked" labelSize="42rpx" iconSize="46rpx" label="自定义大小"></aye-checkbox>
      </demo-block>
      
      <demo-block title="自定义图标">
        <z-checkbox v-model="checked">
          自定义图标
          <template #icon>
            <image
              class="img-icon"
              :src="checked ? activeIcon : inactiveIcon"
            />
          </template>
        </z-checkbox>
      </demo-block>
      <demo-block title="左侧文本">
        <z-checkbox v-model="checked" label-position="left">复选框</z-checkbox>
      </demo-block>
      <demo-block title="禁用文本点击">
        <z-checkbox v-model="checked" label-disabled>复选框</z-checkbox>
      </demo-block>
      
      <demo-block title="复选框组 + 纵向排列">
        <z-checkbox-group v-model="checkedGroup">
          <z-checkbox name="a">复选框 a</z-checkbox>
          <view class="checkbox-content">
            <z-checkbox name="b">复选框 b</z-checkbox>
          </view>
        </z-checkbox-group>
        
        <view class="ma-8"></view>
        <aye-checkbox-group
            v-model="checkedGroup"
            layout="vertical"
            >
              <aye-checkbox label="选项一" value="1" />
              <aye-checkbox label="选项二" value="2" />
              <aye-checkbox label="选项三" value="3" />
            </aye-checkbox-group>
            
      </demo-block>
      
      <demo-block title="水平排列">
        <z-checkbox-group v-model="checkedGroup" direction="horizontal">
          <z-checkbox name="a">复选框 a</z-checkbox>
          <z-checkbox name="b">复选框 b</z-checkbox>
        </z-checkbox-group>
          <view class="ma-12"></view>
          <aye-checkbox-group
              v-model="checkedGroup"
              >
                <aye-checkbox label="选项一" value="1" />
                <aye-checkbox label="选项二" value="2" />
                <aye-checkbox label="选项三" value="3" />
              </aye-checkbox-group>
      </demo-block>
      
      <demo-block title="限制最大可选数">
        <z-checkbox-group v-model="checkedMax" :max="2">
          <z-checkbox name="a">复选框 a</z-checkbox>
          <view class="checkbox-content">
            <z-checkbox name="b">复选框 b</z-checkbox>
          </view>
          <view class="checkbox-content">
            <z-checkbox name="c">复选框 c</z-checkbox>
          </view>
        </z-checkbox-group>
        
        <view class="ma-12"></view>
        <aye-checkbox-group
            v-model="checkedMax2"
            max="2"
            >
              <aye-checkbox label="选项一" value="1" />
              <aye-checkbox label="选项二" value="2" />
              <aye-checkbox label="选项三" value="3" />
            </aye-checkbox-group>
      </demo-block>
      
      <demo-block title="全选与反选">
        <z-checkbox-group v-model="checkedAll" ref="checkboxGroup">
          <z-checkbox name="a">复选框 a</z-checkbox>
          <view class="checkbox-content">
            <z-checkbox name="b">复选框 b</z-checkbox>
          </view>
          <view class="checkbox-content">
            <z-checkbox name="c">复选框 c</z-checkbox>
          </view>
        </z-checkbox-group>
        <view class="button-group">
          <z-button type="primary" size="small" @click="checkAll"
            >全选</z-button
          >
          <view class="button-content">
            <z-button type="primary" size="small" @click="toggleAll"
              >反选</z-button
            >
          </view>
        </view>
        <view class="ma-30"></view>
        <text style="color: var(--greyDark);">纵向排列 + 占满一行 + 两端对齐 + 文字图标反转位置</text>
        <view class="ma-15">
            <aye-checkbox-group
              v-model="checkedAll"
              ref="groupRef"
              layout="vertical"
              vertical-full
              :reverse-vertical-full="true"
              :max="3"
              shape="circle"
            >
              <aye-checkbox label="选项一" value="1" />
              <aye-checkbox label="选项二" value="2" />
              <aye-checkbox label="禁用项（全选反选跳过）" value="3" disabled />
              <aye-checkbox label="选项四" value="4" />
              <aye-checkbox label="选项五" value="5" />
              <aye-checkbox label="选项六" value="6" />
            </aye-checkbox-group>
        
            <view style="margin-top:30rpx;display:flex;gap:20rpx">
              <z-button @tap="$refs.groupRef.selectAll([1,2,3,4,5,6])">全选</z-button>
              <z-button @tap="$refs.groupRef.invertSelect([1,2,3,4,5,6])">反选</z-button>
              <z-button @tap="$refs.groupRef.clearAll()">清空</z-button>
            </view>
          </view>
      </demo-block>
      
      
      <demo-block title="搭配单元格组件使用">
        <z-checkbox-group v-model="checkedCell">
          <z-cell-group>
            <z-cell
              v-for="(item, index) in list"
              clickable
              :key="item"
              :title="`复选框 ${item}`"
              @click="toggle(index)"
            >
              <template #right-icon>
                <z-checkbox
                  :name="item"
                  :ref="(el: any) => (checkboxRefs[index] = el)"
                  @click.stop
                />
              </template>
            </z-cell>
          </z-cell-group>
        </z-checkbox-group>
      </demo-block>
      <demo-block title="不确定状态">
        <z-checkbox
          v-model="isCheckAll"
          :indeterminate="isIndeterminate"
          @change="checkAllChange"
        >
          全选
        </z-checkbox>
        <z-checkbox-group v-model="checkedResult" @change="checkedResultChange">
          <z-checkbox
            v-for="item in listAll"
            :key="item"
            :name="item"
            :custom-style="{ 'margin-top': '20rpx' }"
          >
            复选框 {{ item }}
          </z-checkbox>
        </z-checkbox-group>
      </demo-block>
    </view>
  </DemoPage>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
const checked = ref(true)
const checkedDisabled = ref(true)
const checkDisabled = ref(false)
const checkedShape = ref(['a', 'b'])
const checkedShape2 = ref(false)
const checkedGroup = ref(['a', 'b'])
const checkedMax = ref([])
const checkedMax2 = ref([])
const checkedAll = ref([])
const checkedCell = ref([])
const activeIcon =
  'https://cdn.zebraui.com/zebra-ui/images/assets/demo-select.png'
const inactiveIcon =
  'https://cdn.zebraui.com/zebra-ui/images/assets/demo-noselect.png'
const list = ['a', 'b', 'c']
const listAll = ['a', 'b', 'c', 'd']
const checkboxGroup = ref<any>(null)
const checkAll = () => {
  checkboxGroup.value.toggleAll(true)
}
const toggleAll = () => {
  checkboxGroup.value.toggleAll()
}
const checkboxRefs = ref<any>([])
const toggle = (index: number) => {
  checkboxRefs.value[index].toggle()
}
const isCheckAll = ref(false)
const checkedResult = ref(['a', 'b', 'd'])
const isIndeterminate = ref(true)

const checkAllChange = (val: boolean) => {
  checkedResult.value = val ? listAll : []
  isIndeterminate.value = false
}

const checkedResultChange = (value: string[]) => {
  const checkedCount = value.length
  isCheckAll.value = checkedCount === listAll.length
  isIndeterminate.value = checkedCount > 0 && checkedCount < listAll.length
}
</script>
<style lang="scss" scoped>
.demo-checkbox {
  .checkbox-content {
    margin-top: 20rpx;
  }

  .img-icon {
    width: 40rpx;
    height: 40rpx;
  }

  .button-group {
    display: flex;
    align-items: center;
    margin-top: 30rpx;
  }

  .button-content {
    margin-left: 20rpx;
  }
}
</style>
