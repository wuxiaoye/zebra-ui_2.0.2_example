<template>
    <view class="loading-card"
        :style="{
            flexDirection: props.isVertical ? 'column' : 'row'
        }"
    >
        <view class="item-wrap" 
            :style="{
                margin:  props.isVertical ? '0 0 24rpx 0' : '0 24rpx 0 0'
            }"
        >
              <view class="neu-spinner"
                :style="{
                    width: props.size,
                    height: props.size,
                }"
              ></view>
      </view>
      <text class="forum-caption" v-if="props.isShowText" :style="textStyle">
          <slot>加载中...</slot>
        </text>
    </view>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
    isVertical: {
      type: Boolean,
      default: false
    },
    // 图标大小，必须连带单位一起传入
    size:{
        type: String,
        default: '72rpx'
    },
    isShowText:{
        type: Boolean,
        default: true
    },
    // 文字大小，必须连带单位一起传入
    textSize: {
        type: String,
        default: '24rpx'
    },
    textColor: {
        type: String,
        default: 'var(--zzz-greyDark)'
    }
});


const textStyle = computed(() => {
  const styles = {
    fontSize: props.textSize ,
    color: props.textColor
  }
  return styles
})
</script>

<style scoped>
@keyframes spin {
  to { transform: rotate(360deg); }
}
    
.loading-card {
  display: flex;
  justify-content: center;
  align-items: center;
}
.item-wrap{
    width: 72rpx;
    height: 72rpx;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-shrink: 0;
    box-shadow: var(--zzz-loading4-shadow-item-wrap);
}
.neu-spinner {
    flex-shrink: 0;
  width: 52rpx;
  height: 52rpx;
  border-radius: 50%;
  border: 6rpx solid var(--zzz-loading4-neu-spinner-border-color);
  border-top-color: var(--zzz-primary);
  animation: spin 0.9s linear infinite;
  box-shadow: var(--zzz-loading4-neu-spinner-shadow);
}

.forum-caption {
    font-size: 24rpx;
    color: var(--zzz-loading4-forum-caption-color);
    line-height: 1.5;
}

</style>