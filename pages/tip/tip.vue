<template>
  <view class="page" style="
  background-color: #000; 
  min-height: 100vh;
  ">
    <view class="my-10"></view>

    <!-- 方位选择 -->
    <view class="section-title">1. 弹出方位（切换后点击下方触发）</view>
    <view class="btn-row">
      <z-button size="mini" @click="setPlacement('top-left')">左上</z-button>
      <z-button size="mini" @click="setPlacement('top-right')">右上</z-button>
      <z-button size="mini" @click="setPlacement('bottom-left')">左下(距底100px)</z-button>
      <z-button size="mini" @click="setPlacement('bottom-right')">右下</z-button>
    </view>
    <view class="cur-placement">当前方位：{{ tipPlacement }}</view>

    <view class="my-10"></view>

    <!-- 类型演示 -->
    <view class="section-title">2. 四种类型</view>
    <view class="btn-row">
      <z-button size="mini" @click="fire('default')">默认</z-button>
      <z-button size="mini" @click="fire('success')">成功</z-button>
      <z-button size="mini" @click="fire('warning')">警告</z-button>
      <z-button size="mini" @click="fire('error')">错误</z-button>
    </view>

    <view class="my-10"></view>

    <!-- 极简调用 / 无标题 -->
    <view class="section-title">3. 极简调用（无标题简短消息）</view>
    <view class="btn-row">
      <z-button size="mini" @click="simple">add('这是一条通知')</z-button>
    </view>

    <view class="my-10"></view>

    <!-- 自动关闭 / 永久 -->
    <view class="section-title">4. 自动关闭 vs 永久(手动关闭)</view>
    <view class="btn-row">
      <z-button size="mini" @click="fire('success', 4000)">4秒后自动关闭</z-button>
      <z-button size="mini" @click="fire('error', 0)">永久不关闭(stay:0)</z-button>
    </view>

    <view class="my-10"></view>

    <!-- 操作按钮：弹窗 / 跳转 -->
    <view class="section-title">6. 末尾操作按钮（详情/添加标签）</view>
    <view class="btn-row">
      <z-button size="mini" @click="collectArticle">收藏文章 → 添加标签</z-button>
      <z-button size="mini" @click="showDetail">操作成功 → 查看详情(跳转)</z-button>
    </view>

    <view class="my-10"></view>

    <!-- 批量 -->
    <view class="section-title">7. 连续多条（最多显示9条）</view>
    <view class="btn-row">
      <z-button size="mini" @click="batch">连发 12 条</z-button>
      <z-button size="mini" @click="clearAll">清空全部</z-button>
    </view>

    <!-- 引用组件，placement 可动态切换 -->
    <aye-tip ref="tipRef" :placement="tipPlacement" />

    <!-- 添加标签弹窗（点击通知的“添加标签”按钮唤起） -->
    <z-popup v-model:show="showTagPopup" mode="bottom">
      <view class="tag-pop">
        <view class="tag-pop-title">选择文章标签</view>
        <view class="tag-list">
          <view
            v-for="t in tagOptions"
            :key="t"
            class="tag-item"
            :class="{ active: selectedTags.includes(t) }"
            @click="toggleTag(t)"
          >{{ t }}</view>
        </view>
        <z-button @click="confirmTags">确定</z-button>
      </view>
    </z-popup>
  </view>
</template>

<script>
import ayeTip from "@/components/aye-tip/aye-tip.vue";
export default {
  components: {
    ayeTip,
  },
  data() {
    return {
      tipPlacement: "bottom-right",
      showTagPopup: false,
      tagOptions: ["前端", "后端", "移动端", "设计", "产品", "算法"],
      selectedTags: [],
    };
  },
  methods: {
    // 切换方位
    setPlacement(p) {
      this.tipPlacement = p;
    },

    // 触发一条通知（带标题 + msg）
    fire(type, stay = 5000) {
      const map = {
        default: {  msg: "这是一条普通信息通知，测试：每个组件，包括如下几个部分：以组件名称为标记的开始标签和结束标签、组件内容、组件属性、组件属性值。组件名称由尖括号包裹，称为标签，它有开始标签和结束标签。结束标签的 < 后面用/来表示结束。结束标签也称为闭合标签。" },
        success: { title: "操作成功", msg: "数据已保存并同步至云端" },
        warning: { title: "请注意", msg: "当前操作可能存在风险，请确认" },
        error: { title: "提交失败", msg: "网络异常，请检查网络后重试" },
      };
      const info = map[type] || map.default;
      this.$refs.tipRef.add({
        type,
        title: info.title,
        msg: info.msg,
        stay,
      });
    },

    // 极简调用：无标题简短消息
    simple() {
      this.$refs.tipRef.add("这是一条通知");
    },

    // 连续多条
    batch() {
      const types = ["default", "success", "warning", "error"];
      for (let i = 1; i <= 12; i++) {
        this.$refs.tipRef.add({
          type: types[i % types.length],
          msg: `这是第 ${i} 条测试消息，最多只会显示 9 条`,
          stay: 4000,
        });
      }
    },

    // 清空
    clearAll() {
      this.$refs.tipRef.clearAll();
    },

    // 场景一：收藏文章，通知带“添加标签”按钮，点击唤起大弹窗
    collectArticle() {
        let aa = this;
        
      this.$refs.tipRef.add({
        type: "default",
        // title: "收藏成功",
        msg: "已收藏",
        stay: 0, // 永久，等用户操作
        actionText: "管理分类",
        actionClick: () => {
          aa.showTagPopup = true;
        },
        // 不自动关闭：用户需手动点或关弹窗后处理
        closeAfterAction: true,
      });
    },

    // 场景二：操作成功，通知带“详情”按钮，点击跳转到新页面
    showDetail() {
      this.$refs.tipRef.add({
        type: "success",
        title: "提交成功",
        msg: "资料已审核通过，点详情查看完整记录",
        stay: 6000,
        actionText: "查看详情",
        actionClick: () => {
          uni.navigateTo({ url: "/pages/badge/badge" });
        },
      });
    },

    // 标签弹窗选择
    toggleTag(t) {
      const i = this.selectedTags.indexOf(t);
      if (i >= 0) this.selectedTags.splice(i, 1);
      else this.selectedTags.push(t);
    },

    // 确认标签
    confirmTags() {
      this.showTagPopup = false;
      this.$refs.tipRef.add({
        type: "success",
        msg: `已添加标签：${this.selectedTags.join("、") || "无"}`,
        stay: 4000,
      });
    },
  },
};
</script>

<style scoped>
.page {
  padding: 20rpx;
}
.my-10 {
  height: 20rpx;
}
.section-title {
  font-size: 28rpx;
  font-weight: 600;
  color: #303133;
  margin: 10rpx 0;
}
.btn-row {
  display: flex;
  flex-wrap: wrap;
  gap: 16rpx;
}
.cur-placement {
  font-size: 24rpx;
  color: #909399;
  margin-top: 10rpx;
}
.tag-pop {
  background: #fff;
  border-radius: 20rpx 20rpx 0 0;
  padding: 30rpx;
}
.tag-pop-title {
  font-size: 30rpx;
  font-weight: 600;
  color: #303133;
  margin-bottom: 20rpx;
}
.tag-list {
  display: flex;
  flex-wrap: wrap;
  gap: 16rpx;
  margin-bottom: 30rpx;
}
.tag-item {
  padding: 12rpx 28rpx;
  border-radius: 30rpx;
  background: #f4f4f5;
  color: #606266;
  font-size: 26rpx;
}
.tag-item.active {
  background: #ecf5ff;
  color: #409eff;
}
</style>
