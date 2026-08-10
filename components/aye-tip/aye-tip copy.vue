<template>
  <view class="aye-tip-wrap" :class="[placementClass]">
    <view
      v-for="item in renderList"
      :key="item.id"
      class="aye-tip-item"
      :class="[item.type, item.show ? 'ani-show' : 'ani-hide']"
      :style="getItemStyle(item.index)"
    >
      <!-- 左侧图标 uv-ui -->
      <uv-icon
        class="tip-icon"
        :name="iconMap[item.type]"
        :color="colorMap[item.type]"
        size="36"
      />

      <!-- 文字区域 最多两行 -->
      <view class="tip-text">
        <view class="tip-title">{{ item.title }}</view>
        <view class="tip-desc">{{ item.desc }}</view>
      </view>

      <!-- 自定义操作按钮 -->
      <view
        v-if="item.actionText"
        class="tip-action-btn"
        :style="{ color: colorMap[item.type] }"
        @click.stop="handleAction(item)"
      >
        {{ item.actionText }}
      </view>

      <!-- 关闭按钮 -->
      <uv-icon 
        v-if="item.manualClose"
        class="tip-close"
        name="close"
        size="30"
        color="#c8c9cc"
        @click.stop="closeItem(item.id)"
      />
    </view>
  </view>
</template>

<script>
export default {
  name: "aye-tip",
  data() {
    return {
      // 全部消息队列
      list: [],
      // 最大条数
      maxCount: 9,
      // 单条高度+间距
      itemHeight: 110,
      gap: 16,
      // 动画时长
      aniTime: 300,
      // 图标映射 uv-ui图标
      iconMap: {
        default: "info-circle",
        success: "checkmark-circle",
        warning: "error-circle",
        error: "close-circle",
      },
      // 颜色映射
      colorMap: {
        default: "#409EFF",
        success: "#00b42a",
        warning: "#ff7d00",
        error: "#f53f3f",
      },
    };
  },
  computed: {
    placementClass() {
      return this.placement;
    },
    // 最终渲染列表，截取前9条
    renderList() {
      return this.list.slice(0, this.maxCount);
    },
  },
  props: {
    // 弹出方位：top-left / top-right / bottom-left / bottom-right
    placement: {
      type: String,
      default: "bottom-right",
      validator: (val) => ["top-left", "top-right", "bottom-left", "bottom-right"].includes(val),
    },
  },
  methods: {
    /**
     * 新增消息
     * @param {Object} opt
     * opt.title 标题
     * opt.desc 描述文字（两行截断）
     * opt.type default/success/warning/error
     * opt.stay 自动关闭毫秒，0=永久手动关闭
     * opt.actionText 按钮文字 如：详情、添加标签
     * opt.actionClick 按钮点击回调
     */
    add(opt) {
      const id = Date.now() + Math.random();
      const item = {
        id,
        title: opt.title || "",
        desc: opt.desc || "",
        type: opt.type || "default",
        stay: opt.stay ?? 5000,
        actionText: opt.actionText || "",
        actionClick: opt.actionClick,
        show: false,
        timer: null,
        manualClose: opt.stay <= 0, // 不自动关闭则显示关闭按钮
      };

      // 新消息头部插入
      this.list.unshift(item);

      this.$nextTick(() => {
        item.show = true;
      });

      // 自动关闭定时器
      if (item.stay > 0) {
        item.timer = setTimeout(() => {
          this.closeItem(id);
        }, item.stay);
      }
    },

    // 关闭单条
    closeItem(id) {
      const target = this.list.find((v) => v.id === id);
      if (!target) return;
      clearTimeout(target.timer);
      target.show = false;
      setTimeout(() => {
        this.list = this.list.filter((v) => v.id !== id);
      }, this.aniTime);
    },

    // 操作按钮点击
    handleAction(item) {
      if (typeof item.actionClick === "function") {
        item.actionClick(item);
      }
    },

    // 计算每条top/left偏移
    getItemStyle(index) {
      const offset = index * (this.itemHeight + this.gap);
      const style = {};
      if (this.placement.startsWith("top")) {
        style.top = `${offset}rpx`;
      } else {
        style.bottom = `${offset}rpx`;
      }
      return style;
    },

    // 清空全部
    clearAll() {
      this.list.forEach((item) => clearTimeout(item.timer));
      this.list = [];
    },
  },
  beforeDestroy() {
    // 页面销毁清除所有定时器，防止内存泄漏
    this.list.forEach((item) => clearTimeout(item.timer));
  },
};
</script>

<style scoped>
.aye-tip-wrap {
  position: fixed;
  z-index: 9999;
  pointer-events: none;
}
.bottom-right {
  right: 30rpx;
  bottom: 30rpx;
}
.top-right {
  right: 30rpx;
  top: 30rpx;
}
.bottom-left {
  left: 30rpx;
  bottom: 30rpx;
}
.top-left {
  left: 30rpx;
  top: 30rpx;
}

.aye-tip-item {
  position: absolute;
  width: 81%;
  max-width: 560rpx;
  min-height: 110rpx;
  background: #ffffff;
  border-radius: 12rpx;
  box-shadow: 0 4rpx 30rpx rgba(0, 0, 0, 0.12);
  padding: 24rpx;
  box-sizing: border-box;
  display: flex;
  align-items: flex-start;
  pointer-events: auto;
  transition: all 0.3s ease;
  overflow: hidden;
}

/* 右下角动画：右进右出 */
.bottom-right .ani-hide {
  transform: translateX(120%);
  opacity: 0;
}
.bottom-right .ani-show {
  transform: translateX(0);
  opacity: 1;
}

/* 右上角动画：右进右出 */
.top-right .ani-hide {
  transform: translateX(120%);
  opacity: 0;
}
.top-right .ani-show {
  transform: translateX(0);
  opacity: 1;
}

/* 左下角动画：左进左出 */
.bottom-left .ani-hide {
  transform: translateX(-120%);
  opacity: 0;
}
.bottom-left .ani-show {
  transform: translateX(0);
  opacity: 1;
}

/* 左上角动画：左进左出 */
.top-left .ani-hide {
  transform: translateX(-120%);
  opacity: 0;
}
.top-left .ani-show {
  transform: translateX(0);
  opacity: 1;
}

.tip-icon {
  flex-shrink: 0;
  margin-right: 20rpx;
  margin-top: 4rpx;
}

.tip-text {
  flex: 1;
}
.tip-title {
  font-size: 28rpx;
  color: #303133;
  font-weight: 500;
  line-height: 1.4;
}
.tip-desc {
  font-size: 24rpx;
  color: #606266;
  line-height: 1.5;
  max-height: 72rpx;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  margin-top: 6rpx;
}

.tip-action-btn {
  flex-shrink: 0;
  font-size: 26rpx;
  padding: 0 10rpx;
  line-height: 60rpx;
  white-space: nowrap;
}

.tip-close {
  flex-shrink: 0;
  margin-left: 12rpx;
  margin-top: 2rpx;
}
</style>