<template>
  <view class="aye-tip-wrap" :class="[placement]">
    <view
      v-for="item in renderList"
      :key="item.id"
      class="aye-tip-item"
      :class="[item.type, item.show ? '' : 'ani-hide']"
    >
      <!-- 左侧图标：用纯文本符号，避免依赖外部图标组件 -->
      <view class="tip-icon" :style="{ color: colorMap[item.type] }">{{
        iconMap[item.type]
      }}</view>

      <!-- 文字区域 -->
      <view class="tip-text">
        <view class="tip-title" v-if="item.title">{{ item.title }}</view>
        <view class="tip-desc">{{ item.msg }}</view>
      </view>

        <!-- 末尾操作按钮（详情/添加标签等） -->
        <view
          v-if="item.actionText"
          class="tip-action-btn"
          :style="{ color: colorMap[item.type] }"
          @click.stop="handleAction(item)"
        >{{ item.actionText }}</view>

      <!-- 手动关闭按钮 -->
      <view
        v-if="item.manualClose"
        class="tip-close"
        @click.stop="closeItem(item.id)"
      >×</view>
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
      itemHeight: 130,
      gap: 16,
      // 动画时长
      aniTime: 300,
      // 图标映射（纯文本符号）
      iconMap: {
        default: "i",
        success: "✓",
        warning: "!",
        error: "×",
      },
      // 颜色映射
      colorMap: {
        default: "#0eb805",
        success: "#0eb805",
        warning: "#ff7d00",
        error: "#f53f3f",
      },
    };
  },
  computed: {
    // 最终渲染列表，截取前9条
    renderList() {
      return this.list.slice(0, this.maxCount);
    },
  },
  props: {
    // 弹出方位：top-left / top-right / bottom-left / bottom-right
    placement: {
      type: String,
      default: "top-left",
      validator: (val) =>
        ["top-left", "top-right", "bottom-left", "bottom-right"].includes(val),
    },
  },
  methods: {
    /**
     * 新增消息
     * @param {String|Object} opt
     * 极简调用：add('这是一条通知')
     * 对象调用：
     *   opt.title 标题（不设置则隐藏标题）
     *   opt.msg   消息正文
     *   opt.type  default/success/warning/error
     *   opt.stay  自动关闭毫秒，0=永久
     *   opt.manualClose 是否显示关闭按钮
     *   opt.actionText 末尾操作按钮文字，如：详情、添加标签
     *   opt.actionClick 按钮点击回调(item)，可弹窗或跳转
     *   opt.closeAfterAction 点击按钮后是否自动关闭该通知，默认 true
     */
    add(opt) {
      // 支持字符串极简调用
      if (typeof opt === "string") {
        opt = { msg: opt };
      }
      const id = Date.now() + Math.random();
      const item = {
        id,
        title: opt.title || "",
        msg: opt.msg || "",
        type: opt.type || "default",
        stay: opt.stay ?? 5000,
        // 是否显示手动关闭按钮（stay<=0 或显式指定）
        manualClose: opt.stay <= 0 || opt.manualClose || false,
        // 末尾操作按钮
        actionText: opt.actionText || "",
        actionClick: opt.actionClick,
        closeAfterAction: opt.closeAfterAction ?? true,
        // 首帧即显示态，避免真机首条卡在 opacity:0
        show: true,
        timer: null,
      };

      // 新消息头部插入
      this.list.unshift(item);

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
      // 点击后默认自动关闭该通知
      if (item.closeAfterAction) {
        this.closeItem(item.id);
      }
    },

    // 计算每条偏移（flex 已处理堆叠，这里返回空，避免干扰定位）
    getItemStyle() {
      return {};
    },

    // 清空全部
    clearAll() {
      this.list.forEach((item) => clearTimeout(item.timer));
      this.list = [];
    },
  },
  beforeDestroy() {
    // 组件销毁清除所有定时器，防止内存泄漏
    this.list.forEach((item) => clearTimeout(item.timer));
  },
};
</script>

<style scoped>
/* 外层铺满，用 flex 控制通知框停靠的角 */
.aye-tip-wrap {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 9999;
  pointer-events: none;
  display: flex;
  flex-direction: column;
  padding: 30rpx;
  box-sizing: border-box;
}
/* 左上：靠上靠左 */
.top-left {
  align-items: flex-start;
  justify-content: flex-start;
}
/* 右上：靠上靠右 */
.top-right {
  align-items: flex-end;
  justify-content: flex-start;
}
/* 右下：靠下靠右，距底 150px（300rpx - 外层30rpx = 270rpx） */
.bottom-right {
  align-items: flex-end;
  justify-content: flex-end;
  padding-bottom: 150px;
}
/* 左下：靠下靠左，距底 150px（300rpx - 外层30rpx = 270rpx） */
.bottom-left {
  align-items: flex-start;
  justify-content: flex-end;
  padding-bottom: 150px;
}

/* 右侧两类：从右到左划入，使用反向动画 */
.top-right .aye-tip-item,
.bottom-right .aye-tip-item {
  animation-name: aye-tip-in-right;
}
.top-right .ani-hide,
.bottom-right .ani-hide {
  transform: translateX(120%);
}

@keyframes aye-tip-in-right {
  from {
    opacity: 0;
    transform: translateX(120%);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.aye-tip-item {
  width: 81%;
  max-width: 560rpx;
  background: #000;
  border-radius: 12rpx;
  box-shadow: 0 4rpx 30rpx rgba(0, 0, 0, 0.12);
  padding: 24rpx;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  margin: 16rpx 0;
  pointer-events: auto;
  /* 退场过渡 */
  transition: opacity 0.3s ease, transform 0.3s ease;
  /* 进场动画：每次插入元素自动播放（从左到右划入） */
  animation: aye-tip-in 0.3s ease both;
  box-shadow: 3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
}

@keyframes aye-tip-in {
  from {
    opacity: 0;
    transform: translateX(-120%);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* 退场：反向滑回左侧 */
.ani-hide {
  opacity: 0;
  transform: translateX(-120%);
}

.tip-icon {
  flex-shrink: 0;
  width: 40rpx;
  height: 40rpx;
  line-height: 40rpx;
  text-align: center;
  font-size: 26rpx;
  font-weight: bold;
  margin-right: 20rpx;
  border: 2rpx solid currentColor;
  border-radius: 50%;
  box-sizing: border-box;
}

.tip-text {
  flex: 1;
}
.tip-close {
  flex-shrink: 0;
  width: 40rpx;
  height: 40rpx;
  line-height: 40rpx;
  text-align: center;
  font-size: 36rpx;
  color: #c8c9cc;
  margin-left: 12rpx;
  margin-top: -4rpx;
}
.tip-title {
  font-size: 28rpx;
  color: #e7e7e7;
  font-weight: 500;
  line-height: 1.4;
  margin-bottom: 6rpx;
}
.tip-desc {
  font-size: 24rpx;
  color: #fff;
  line-height: 1.5;
  max-height: 66rpx;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
.tip-action-btn {
  /* display: inline-block; */
  /* margin-top: 14rpx; */
  min-width: 0;
  flex-shrink: 0;
  font-size: 24rpx;
  font-weight: 500;
  line-height: 1.4;
  color: #00ce63;
}
</style>
