<template>
    <view class="pt-10 pb-30" style="background-color: var(--zzz-greyLight-1); min-height: 100vh; ">
        
        <view v-for="( obj , obj_index ) in mList">
            <view class="py-10 px-20 text-greyDark text-size-s">{{obj.title}}</view>
            
            <z-row v-for="( item, index ) in obj.list" >
              <z-col span="10" >
                  <z-tag type="primary" none-border>{{item.name}}</z-tag>
                </z-col>
              <z-col span="7"  class="text-align-center"
                    :style="riStyle(item)"
              >
                  白天文字
               </z-col>
              <z-col span="7" style="background-color: #000 ;" class="text-align-center"
                :style="yeStyle(item)"
              >
                  夜间文字
              </z-col>
            </z-row>
        </view>
    </view>
</template>

<script setup>
    import { ref, computed } from 'vue';
    
    const mList = ref([
        {
            title: '比基准灰色更黑',
            list: [
                { name: '--zzz-ri-hei_ye-bai-1', ri: '#131313', ye: '#f3f3f3' },
                { name: '--zzz-ri-hei_ye-bai-2', ri: '#333', ye: '#dedede' },
                { name: '--zzz-ri-hei_ye-bai-3', ri: '#6f7c94', ye: '#bfbfbf' },
                { name: '--zzz-ri-hei_ye-bai-4', ri: '#7988a2', ye: '#aaa5a7' },
                { name: '--zzz-ri-hei_ye-bai-5', ri: 'var(--zzz-greyDark-3)', ye: '#bfbfbf' },
            ]
        },
        {
            title: '基准灰色',
            list: [
                { name: '--zzz-ri-hui_ye-lv', ri: '#92a1c3', ye: 'var(--zzz-primary)' },
                { name: '--zzz-ri-ye-tong-hui', ri: 'var(--zzz-greyDark)', ye: '#9baacf' },
                { name: '--zzz-ri-hui_ye-hui-1', ri: '#92a1c3', ye: '#c1babc' },
                { name: '--zzz-ri-hui_ye-hui-2', ri: 'var(--zzz-greyDark)', ye: '#7f7f7f' },
            ]
        },
        {
            title: '比基准灰色更淡',
            list: [
                { name: '--zzz-ri-bai_ye-hei-1', ri: '#aec3e3', ye: '#7f7f7f' },
                { name: '--zzz-ri-bai_ye-hei-2', ri: '#aec3e3', ye: '#4f4f4f' },
                
                { name: '--zzz-ri-bai_ye-hei-3', ri: '#a3a3a3', ye: '#7f7f7f' },
                { name: '--zzz-ri-bai_ye-hei-4', ri: '#a3a3a3', ye: '#4f4f4f' },
                
                { name: '--zzz-ri-bai_ye-hei-5', ri: '#c3c3c3', ye: '#7f7f7f' },
                { name: '--zzz-ri-bai_ye-hei-6', ri: '#c3c3c3', ye: '#4f4f4f' },
            ]
        },
        {
            title: '非常淡 - 可能用于：禁用状态',
            list: [
                { name: '--zzz-ri-ji-bai_ye-ji-hei-1', ri: '#c8d0e7', ye: '#444'  , ye_background:'#191919' },
                { name: '--zzz-ri-ji-bai_ye-ji-hei-2', ri: '#b8cdf4', ye: '#444' , ye_background:'#191919' },
                
                
                { name: '--zzz-ri-ji-bai_ye-ji-hei-3', ri: '#d8e4f5', ye: '#444'  , ye_background:'#191919' },
                //日历组件会用到
                { name: '--zzz-ri-ji-bai_ye-ji-hei-4', ri: '#f5f5f7', ye: '#2a2a2d' },
            ]
        },
        {
            title: '绿底白字',
            list: [
                { 
                    name: '--zzz-lv-di-bai-zi', 
                    ri: '#f3f3f3',  ye: '#f3f3f3' ,
                    ri_background: 'var(--zzz-primary)',
                    ye_background: 'var(--zzz-primary)'
                },
            ]
        },
        {
            title: '其他',
            list: [
                { name: '--z-text-color', ri: 'var(--z-text-color)', ye: '#f5f5f5' },
                { name: '--z-text-color-2', ri: 'var(--z-text-color-2)', ye: '#707070' },
                { name: '--z-text-color-3', ri: 'var(--z-text-color-3)', ye: '#4d4d4d' },
                { name: '--z-active-color', ri: 'var(--z-active-color)', ye: '#3a3a3c' },
                { name: '--z-background', ri: 'var(--z-background)', ye: '#000' },
                { name: '--z-background-2', ri: 'var(--z-background-2)', ye: '#191919' },
                { name: '--z-background-3', ri: 'var(--z-background-3)', ye: '#37363b' },
            ]
        },
        {
            title: '灰色',
            list: [
                { name: '--z-gray-1', ri: 'var(--z-gray-1)', ye: '#f7f8fa' },
                { name: '--z-gray-2', ri: 'var(--z-gray-2)', ye: '#f2f3f5' },
                { name: '--z-gray-3', ri: 'var(--z-gray-3)', ye: '#ebedf0' },
                { name: '--z-gray-4', ri: 'var(--z-gray-4)', ye: '#dcdee0' },
                { name: '--z-gray-5', ri: 'var(--z-gray-5)', ye: '#9baacf' },
                { name: '--z-gray-6', ri: 'var(--z-gray-6)', ye: '#969799' },
                { name: '--z-gray-7', ri: 'var(--z-gray-7)', ye: '#646566' },
                { name: '--z-gray-8', ri: 'var(--z-gray-8)', ye: '#333' },
            ]
        },
    ])
    
    //白天
    const riStyle = (item)=>{
        const style = { }
        style.color = item.ri;
        if(item.ri_background){
            style.background = item.ri_background
        }
        return style;
    }
    
    //夜间
    const yeStyle = (item)=>{
        const style = { }
        style.color = item.ye;
        if(item.ye_background){
            style.background = item.ye_background
        }
        return style;
    }
</script>

<style>
           
</style>
