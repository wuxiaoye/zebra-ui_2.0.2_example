<template>
  <DemoPage title="Area">
    <view class="demo-area">
      <demo-block title="基础用法" :box-shadow="false">
        <z-area title="标题" :area-list="areaList" class="add_shadow round-12 overflow"/>
      </demo-block>
      
      <demo-block title="控制选中项" :box-shadow="false">
        <z-area v-model="valueSelect" title="标题" :area-list="areaList"  class="add_shadow round-12 overflow"/>
      </demo-block>
      
      <demo-block title="配置显示列" :box-shadow="false">
        <z-area title="标题" :area-list="areaList" :columns-num="2"  class="add_shadow round-12 overflow"/>
      </demo-block>
      
      <demo-block title="配置列占位提示文字" :box-shadow="false">
        <z-area
          title="标题"
          :area-list="areaList"
          :columns-placeholder="['请选择', '请选择', '请选择']"
         class="add_shadow round-12 overflow"/>
      </demo-block>
    </view>
  </DemoPage>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import { areaList } from '../../common/js/area'
const valueSelect = ref('330302')
</script>
