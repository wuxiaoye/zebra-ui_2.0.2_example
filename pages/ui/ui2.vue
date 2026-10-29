<template>
  <view class="container">
      <!-- 头像颜色列表 -->
      <view>
          <view class="text-greyDark text-size-n">头像组件</view>
          <view style="margin-top: 20rpx; margin-left: 10rpx;">单色 21种</view>
          <view style="display: flex; flex-direction: row; flex-wrap: wrap;">
              <aye-avatar size="35" v-for="(item, index) in 21"  :text="String( index +1 )" :bgColorIndex="index" style="margin-top: 10px; margin-right: 10rpx; " />
          </view>
          
          <view style="margin-top: 20rpx; margin-left: 10rpx;">双色 49种</view>
          <view style="display: flex; flex-direction: row; flex-wrap: wrap;">
              <aye-avatar size="35" 
                  v-for="num in Array.from({length: 70 - 21}, (_, i) => 21 + i)" 
                  :text="String(num +1)" 
                  :bgColorIndex="num" style="margin-top: 10px; margin-right: 10rpx; " />
          </view>
          
          <view style="margin-top: 20rpx; margin-left: 10rpx;">三色 56种</view>
          <view style="display: flex; flex-direction: row; flex-wrap: wrap;">
              <aye-avatar size="35"  
                  v-for="num in Array.from({length: 126 - 70 }, (_, i) => 70 + i)"
                  :text="String(num +1)" 
                  :bgColorIndex="num" style="margin-top: 10px; margin-right: 10rpx; " />
          </view>
      </view>
      
    <view style="margin-top: 40px;"></view>
    <view class="components">
        <!-- 单选框 -->
        <view class="radio">
          <z-radio2 v-model="radio" value="1" label="红枣"/>
          <z-radio2 v-model="radio" value="2" label="蜜蜂" />
        </view>
        <view style="padding:30rpx">
            <!-- 竖向排列 + 整行铺满 + 文字左圆点右 -->
            <z-radio-group2
              v-model="radio_selectedVal"
              layout="vertical"
              vertical-full
              reverse-align
              @change="radio_groupChange"
            >
              <z-radio2 label="选项A" value="A" />
              <z-radio2 label="选项B（禁用）" value="B" disabled />
              <z-radio2 label="选项C" value="C" />
              <z-radio2 label="选项D" value="D" />
              <z-radio2 label="选项E" value="E" />
            </z-radio-group2>
        
            <view style="margin-top:40rpx">当前选中：{{ radio_selectedVal }}</view>
          </view>
        
      <!-- 开关 -->
      <view class="switch">
        <z-switch2  v-model="switch1"></z-switch2>
        <z-switch2 v-model="switch2" />
      </view>

      <!-- 复选框 -->
      <view class="checkbox">
        <z-checkbox2  v-model="checkbox1" label="菊花" />
        <z-checkbox2 v-model="checkbox2" label="金银花" />
      </view>
      
      <view class="ma-30">
        <view>===== 单独使用单个Checkbox =====</view>
            <z-checkbox2
              v-model="singleCheck"
              label="单独选项"
              icon-size="30rpx"
              label-size="44rpx"
              label-color="#aa00ff"
              active-icon-color="#2fc7e5"
            />
        
            <view style="margin:40rpx 0">===== Group多选组（横向）=====</view>
            <z-checkbox-group2
              v-model="checkList"
              ref="checkboxGroupRef"
              :max="3"
              layout="horizontal"
              shape="circle"
              icon-size="42rpx"
               @change="handleGroupChange"
            >
              <z-checkbox2 label="苹果" value="apple" disabled />
              <z-checkbox2 label="香蕉" value="banana" @change="handleSingleChange" />
              <z-checkbox2 label="橙子" value="orange" />
              <z-checkbox2 label="葡萄" value="grape" />
              <z-checkbox2 label="菊花" value="a1" />
              <z-checkbox2 label="罗汉果" value="a2" />
              <z-checkbox2 label="玫瑰花" value="a3" />
            </z-checkbox-group2>
        
            <view class="my-15">已选中：{{ checkList }}</view>
            <view style="margin:30rpx 0;display:flex;gap:20rpx">
              <button @tap="handleAll">全选</button>
              <button @tap="handleInvert">反选</button>
              <button @tap="handleClear">清空</button>
            </view>
        
            <view style="margin:40rpx 0">===== Group竖向排列，item占满一行两端对齐 =====</view>
            <z-checkbox-group2
              v-model="checkList2"
              layout="vertical"
              :vertical-full="true"
              :reverse-vertical-full="true"
            >
              <z-checkbox2
                label="竖向选项1"
                value="v1"
              />
              <z-checkbox2
                label="竖向选项2"
                value="v2"
              />
              <z-checkbox2
                label="竖向选项3"
                value="v3"
                layout="vertical"
                :vertical-full="true"
                shape="circle"
              />
            </z-checkbox-group2>
        
      </view>

      

      <!-- 按钮 -->
      <view style="display: flex; flex-direction: column; justify-content: center; align-items: center; gap: 20px;">
          
      <aye-button type="primary" label="Primary" @click="handleClick" />
      <aye-button type="secondary" label="Secondary" @click="handleClick" />
      <aye-button type="change-up" label="斜向上动画" v-model="btnActive" />
      <aye-button type="change-upward" label="从下到上动画" v-model="btnActive" />
      <aye-button type="change-color" label="缓缓变色动画" v-model="btnActive" />
      
          <aye-button type="change-up" size="mini" v-model="btnActive" label="迷你" />
          <aye-button type="change-color" size="small" v-model="btnActive" label="小号" />
          <aye-button type="secondary" label="中等" />
          <aye-button type="primary" size="large" label="超大" />
          
          <aye-button
            type="change-up"
              v-model="btnActive"
              label="自定义样式按钮"
              custom-padding="30rpx 60rpx"
              custom-font-size="38rpx"
              custom-radius="40rpx"
          />
          
          <aye-button
            type="secondary"
            label="全圆角按钮"
            custom-padding="24rpx"
            custom-radius="999rpx"
          />
      </view>


      <!-- 社交媒体按钮 -->
      <view class="social-buttons">
        <aye-social-button  icon="home-fill"  v-model="socialActive" />
        <aye-social-button  icon="account-fill"  v-model="socialActive" />
        <aye-social-button  icon="setting-fill" v-model="socialActive" />
      </view>
      <view class="social-buttons">
          <aye-social-button v-model="socialActive" />
          <aye-social-button
            v-model="socialActive"
            round
            text=""
            activeBgColor="#f56c6c"
          />
          <aye-social-button
            v-model="socialActive"
            radius="30rpx"
            width="220rpx"
            height="80rpx"
            text="提交表单"
            textColor="#333"
            activeTextColor="#fff"
            activeBgColor="#409eff"
          />
          <aye-social-button
            v-model="socialActive"
            icon=""
            text="点击切换"
          />
      </view>

      <!-- 时钟 -->
      <aye-clock />

      <!-- 圆形播放按钮 -->
      <aye-play-button v-model="isPlaying" />

      <!-- 输入框 -->
      <aye-input v-model="inputText"  />

      <!-- 搜索框 -->
      <aye-search-input v-model="searchText" />

      

      <!-- 圆形图标按钮 -->
      <view class="icon">
        <aye-icon-button icon="home-fill" @click="onIconClick('home')" />
        <aye-icon-button icon="account-fill" @click="onIconClick('account')" />
        <aye-icon-button icon="setting-fill" @click="onIconClick('setting')" />
      </view>

      <!-- 进度条滑块 -->
      <z-slider v-model="sliderValue" show-tip />
    </view>
    
    <view style="width: 100%; height: 50px;"></view>
    <!-- Tab 切换 -->
    <z-tabbar2 v-model="tabIndex" :tabs="['Tab 1', 'Tab 2', 'Tab 3', 'Tab 4']" />
    <view style="width: 100%; height: 50px;"></view>
    <!-- 4 个 Tab -->
        <z-tabbar2 v-model="tabIndex2" :tabs="['首页', '分类', '购物车', '我的', 'Tab 5']" />
    
    <view style="width: 100%; height: 50px;"></view>
  </view>
</template>

<script setup>
import { ref } from 'vue';

// 状态
const switch1 = ref(false);
const switch2 = ref(true);
const checkbox1 = ref(false);
const checkbox2 = ref(true);
const radio = ref('2');
const btnActive = ref(false);
const socialActive = ref(false);
const isPlaying = ref(true);
const inputText = ref('');
const searchText = ref('');
const tabIndex = ref(0);
const tabIndex2 = ref(0);
const sliderValue = ref(50);

// 事件处理
const handleClick = () => console.log('按钮点击');
const onIconClick = (name) => console.log('图标点击:', name);

// 多选框
// 多选组绑定值
let checkList = ref([])
let checkList2 = ref([])
// 所有可选项，用于全选/反选
const allOptions = ['apple', 'banana', 'orange', 'grape']

// 组件实例，调用全选反选
let checkboxGroupRef = ref(null)

// 全选
const handleAll = () => {
  checkboxGroupRef.value.selectAll(allOptions)
}
// 反选
const handleInvert = () => {
  checkboxGroupRef.value.invertSelect(allOptions)
}
// 清空
const handleClear = () => {
  checkboxGroupRef.value.clearAll()
}

// 单独单个checkbox
let singleCheck = ref(false)

const handleSingleChange = (val, checked) => {
  console.log('点击了选项', val, '是否选中', checked)
}
// 单选点击、全选、反选、清空都会触发
const handleGroupChange = (selectedArr) => {
  console.log('组最新选中数组：', selectedArr)
}

// 单选项
const radio_selectedVal = ref('A')
// 组change事件
const  radio_groupChange = (val) => {
  console.log('单选组选中值：', val)
}

</script>

<style>
/* 全局样式（页面布局） */
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
  --primary-light: #2fe25f;
  --primary: #07c160;
  --primary-dark: #0eb805;
}
page {
  background: var(--greyLight-1);
  font-size: 16rpx;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: var(--greyLight-1);
  padding: 40rpx;
  padding-bottom: 120rpx;
}
.components {
  width: 80%;
  border-radius: 60rpx;
  box-shadow: 16rpx 16rpx 28rpx var(--greyLight-2), -4rpx -4rpx 36rpx var(--white);
  padding: 40rpx;
  display: grid;
  grid-template-columns: 1fr;
  grid-row-gap: 40rpx;
  align-items: center;
}
.switch {
  display: grid;
  grid-template-columns: repeat(2, min-content);
  grid-gap: 60rpx;
  justify-self: center;
}
.checkbox {
  display: grid;
  /* grid-template-columns: repeat(2, 120rpx); */
  grid-gap: 30rpx;
  justify-content: center;
}
.radio {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  justify-items: center;
}
.social-buttons {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: flex-start;
  gap: 20rpx;
  padding: 20rpx 0;
  margin-top: 30rpx;
}
.icon {
  display: flex;
  justify-content: space-between;
}
.add-shadow {
  box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
}

</style>