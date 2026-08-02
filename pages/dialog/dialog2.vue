<template>
  <view>
    <view class="ma-n20">
      <button @click="openDialog">打开提示弹窗</button>
    </view>

    <!-- 重点：必须加 use-component 属性！！ -->
    <z-dialog
      :show="dialogVisible"
      use-component
      title="标题"
      message="这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。这是一个示例提示。"
      :show-cancel-button="true"
      @confirm="handleConfirm"
      @cancel="handleCancel"
      
    />
      <!-- @update:show="val => dialogVisible = val" -->
  </view>
</template>

<script>
export default {
  data() {
    return {
      dialogVisible: false
    }
  },
  methods: {
    openDialog() {
      this.dialogVisible = true
      console.log('弹窗已开启', this.dialogVisible)
    },
    // 确认回调 正常打印日志
    handleConfirm() {
      console.log('点击了确认')
      this.dialogVisible = false
    },
    // 取消回调 正常打印日志
    handleCancel() {
      console.log('点击了取消')
      this.dialogVisible = false
    }
  }
}
</script>

<style>
</style>