<template>
  <view class="ui-components-page">
      <!-- 顶部状态栏 -->
      <view style=" height: var(--status-bar-height);"></view>
    <!-- 0. Page Header -->
    <view class="comp-section">
      <view class="header-box">
        <view class="header-icon">
          <uv-icon name="grid" :size="20" color="#fff"></uv-icon>
        </view>
        <view class="header-text">
          <text class="forum-h3">UI 组件库</text>
          <text class="forum-caption">Mobile Forum APP · Neumorphic Style</text>
        </view>
      </view>
    </view>
    
    <view>
        <view class="ma-40">cell 单元格</view>
        <view class="ma-40">基本用法</view>
        <z-cell-group class="add_shadow">
          <z-cell title="单元格" value="内容" />
          <z-cell title="单元格" value="内容" label="描述信息" />
          <z-cell title="单元格" value="内容" />
          <z-cell title="单元格" value="内容" />
        </z-cell-group>
        
        <view class="ma-40">卡片风格</view>
        <z-cell-group  title="分组1" inset>
          <z-cell title="单元格" value="内容"  icon="appstore" />
          <z-cell title="单元格" value="内容" label="描述信息" center />
          <z-cell title="单元格" value="内容" />
          <z-cell value="内容" is-link>
            <!-- 使用 title 插槽来自定义标题 -->
            <template #title>
              <text class="custom-title">单元格</text>
              <z-tag type="primary">标签</z-tag>
            </template>
          </z-cell>
          
          <z-cell title="单元格" icon="creditcard">
            <!-- 使用 right-icon 插槽来自定义右侧图标 -->
            <template #right-icon>
              <z-icon name="search" class="search-icon" />
            </template>
          </z-cell>
        </z-cell-group>
        <view class="ma-40"></view>
        <z-cell-group title="分组2" inset>
          <z-cell title="单元格" value="内容"  icon="appstore"/>
          <z-cell center title="标题">
            <template #right-icon>
              <z-switch2 v-model="checked"></z-switch2>
            </template>
          </z-cell>
          <z-cell title="单元格" value="内容" is-link/>
          <z-cell title="单元格" value="内容" label="描述信息" />
          <z-cell title="单元格" value="内容" />
        </z-cell-group>
        
    </view>
    
    <view class="ma-20"></view>
    <!-- 卡片 -->
    <view class="author-box add_shadow" >
        <view class="author-box__title" >
            <text class="title">帖主</text>
        </view>
        <view class="author ">
            <view class="author-info" >
                <view class="avatar-pic">
                    <aye-avatar size="32" text="道德经好" randomBgColor/>
                </view>
                <view class="author-name">
                    岐黄传承岐黄传承岐黄传承
                </view>
            </view>
            <view class="btn-list">
                <aye-social-button  
                    round
                    icon="checkbox-mark"
                    iconColor="var(--primary)"
                    width="26px"
                    height="26px"
                />
                <aye-button type="change-up"  size="mini" label="关注" />
                
                <view class="btn-item" 
                    hover-class="hover-press"
                    hover-stay-time="500">
                        <uv-icon name="share2" custom-prefix="aye-icon" size="16px"></uv-icon>
                </view>
            </view>
        </view>
    </view>

    <!-- 1. 骨架屏 Skeleton -->
    <view class="comp-section">
      <text class="comp-label">1. 骨架屏 Skeleton</text>
      <view class="neu-card skeleton-card">
        <view class="skeleton-header">
          <view class="skeleton-bar skeleton-avatar"></view>
          <view class="skeleton-info">
            <view class="skeleton-bar skeleton-title"></view>
            <view class="skeleton-bar skeleton-subtitle"></view>
          </view>
        </view>
        <view class="skeleton-bar skeleton-line"></view>
        <view class="skeleton-bar skeleton-line short"></view>
        <view class="skeleton-bar skeleton-line shorter"></view>
      </view>
    </view>

    <!-- 2. 日历 Calendar -->
    <view class="comp-section">
      <text class="comp-label">2. 日历 Calendar</text>
      <view class="neu-card calendar-card">
        <view class="calendar-header">
          <uv-icon name="arrow-left" :size="18" color="#9baacf"></uv-icon>
          <text class="forum-h4">2026 年 7 月</text>
          <uv-icon name="arrow-right" :size="18" color="#9baacf"></uv-icon>
        </view>
        <view class="calendar-weekdays">
          <text class="forum-caption weekday">日</text>
          <text class="forum-caption weekday">一</text>
          <text class="forum-caption weekday">二</text>
          <text class="forum-caption weekday">三</text>
          <text class="forum-caption weekday">四</text>
          <text class="forum-caption weekday">五</text>
          <text class="forum-caption weekday">六</text>
        </view>
        <view class="calendar-grid">
          <view class="cal-cell other-month">29</view>
          <view class="cal-cell other-month">30</view>
          <view class="cal-cell">1</view>
          <view class="cal-cell">2</view>
          <view class="cal-cell">3</view>
          <view class="cal-cell">4</view>
          <view class="cal-cell">5</view>
          <view class="cal-cell">6</view>
          <view class="cal-cell">7</view>
          <view class="cal-cell">8</view>
          <view class="cal-cell">9</view>
          <view class="cal-cell">10</view>
          <view class="cal-cell">11</view>
          <view class="cal-cell">12</view>
          <view class="cal-cell">13</view>
          <view class="cal-cell">14</view>
          <view class="cal-cell">15</view>
          <view class="cal-cell">16</view>
          <view class="cal-cell">17</view>
          <view class="cal-cell">18</view>
          <view class="cal-cell">19</view>
          <view class="cal-cell today">20</view>
          <view class="cal-cell">21</view>
          <view class="cal-cell">22</view>
          <view class="cal-cell">23</view>
          <view class="cal-cell">24</view>
          <view class="cal-cell">25</view>
          <view class="cal-cell">26</view>
          <view class="cal-cell">27</view>
          <view class="cal-cell">28</view>
          <view class="cal-cell">29</view>
          <view class="cal-cell">30</view>
          <view class="cal-cell">31</view>
          <view class="cal-cell other-month">1</view>
          <view class="cal-cell other-month">2</view>
        </view>
      </view>
    </view>

    <!-- 3. 下拉筛选 Dropdown Filter -->
    <view class="comp-section">
      <text class="comp-label">3. 下拉筛选 Dropdown Filter</text>
      <view class="dropdown-row">
        <view class="neu-card dropdown-item">
          <text class="forum-body">全部分类</text>
          <uv-icon name="arrow-down" :size="14" color="#9baacf"></uv-icon>
        </view>
        <view class="neu-card dropdown-item">
          <text class="forum-body">最新发布</text>
          <uv-icon name="arrow-down" :size="14" color="#9baacf"></uv-icon>
        </view>
      </view>
    </view>

    <!-- 4. 垂直选项卡 Vertical Tabs -->
    <view class="comp-section">
      <text class="comp-label">4. 垂直选项卡 Vertical Tabs</text>
      <view class="neu-card vertical-tabs">
        <view class="tabs-sidebar">
          <view class="tab-item active">
            <uv-icon name="home" :size="16" color="#fff"></uv-icon>
            <text class="tab-text">首页</text>
          </view>
          <view class="tab-item">
            <uv-icon name="eye" :size="16" color="#9baacf"></uv-icon>
            <text class="tab-text">发现</text>
          </view>
          <view class="tab-item">
            <uv-icon name="bell" :size="16" color="#9baacf"></uv-icon>
            <text class="tab-text">消息</text>
          </view>
          <view class="tab-item">
            <uv-icon name="account" :size="16" color="#9baacf"></uv-icon>
            <text class="tab-text">我的</text>
          </view>
        </view>
        <view class="tabs-content">
          <text class="forum-body">首页内容区域</text>
          <view class="content-items">
            <view class="neu-flat-sm content-item">
              <text class="caption-text">热门话题</text>
            </view>
            <view class="neu-flat-sm content-item">
              <text class="caption-text">最新动态</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- 5. 瀑布流 Waterfall -->
    <view class="comp-section">
      <text class="comp-label">5. 瀑布流 Waterfall</text>
      <view class="waterfall">
        <view class="waterfall-item">
          <view class="neu-card waterfall-card">
            <view class="waterfall-image" style="background: linear-gradient(135deg, #07c160, #2fe25f);"></view>
            <view class="waterfall-content">
              <view class="forum-body">周末徒步活动</view>
              <view class="forum-caption">小明</view>
            </view>
          </view>
        </view>
        <view class="waterfall-item">
          <view class="neu-card waterfall-card">
            <view class="waterfall-image tall" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);"></view>
            <view class="waterfall-content">
              <view class="forum-body">设计灵感分享</view>
              <view class="forum-caption">设计师阿花</view>
            </view>
          </view>
        </view>
        <view class="waterfall-item">
          <view class="neu-card waterfall-card">
            <view class="waterfall-image short" style="background: linear-gradient(135deg, #f59e0b, #fcd34d);"></view>
            <view class="waterfall-content">
              <view class="forum-body">美食探店记录</view>
              <view class="forum-caption">吃货联盟</view>
            </view>
          </view>
        </view>
        <view class="waterfall-item">
          <view class="neu-card waterfall-card">
            <view class="waterfall-image medium" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);"></view>
            <view class="waterfall-content">
              <view class="forum-body">读书笔记整理</view>
              <view class="forum-caption">书虫小组</view>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- 6. 图标 Icons -->
    <view class="comp-section">
      <text class="comp-label">6. 图标 Icons</text>
      <view class="icon-grid">
        <view class="neu-flat-sm icon-item">
          <uv-icon name="home" :size="22" color="#07c160"></uv-icon>
          <text class="icon-label">首页</text>
        </view>
        <view class="neu-flat-sm icon-item">
          <uv-icon name="search" :size="22" color="#07c160"></uv-icon>
          <text class="icon-label">搜索</text>
        </view>
        <view class="neu-flat-sm icon-item">
          <uv-icon name="account" :size="22" color="#07c160"></uv-icon>
          <text class="icon-label">用户</text>
        </view>
        <view class="neu-flat-sm icon-item">
          <uv-icon name="heart" :size="22" color="#ef4444"></uv-icon>
          <text class="icon-label">收藏</text>
        </view>
        <view class="neu-flat-sm icon-item">
          <uv-icon name="chat" :size="22" color="#6d5dfc"></uv-icon>
          <text class="icon-label">消息</text>
        </view>
        <view class="neu-flat-sm icon-item">
          <uv-icon name="setting" :size="22" color="#9baacf"></uv-icon>
          <text class="icon-label">设置</text>
        </view>
        <view class="neu-flat-sm icon-item">
          <uv-icon name="share" :size="22" color="#9baacf"></uv-icon>
          <text class="icon-label">分享</text>
        </view>
        <view class="neu-flat-sm icon-item">
          <uv-icon name="star" :size="22" color="#f59e0b"></uv-icon>
          <text class="icon-label">收藏</text>
        </view>
      </view>
    </view>

    <!-- 7. 按钮 Buttons -->
    <view class="comp-section">
      <text class="comp-label">7. 按钮 Buttons</text>
      <view class="button-group">
        <view class="button-row">
          <view class="neu-primary-btn button-primary">
            <text class="button-text">主要按钮</text>
          </view>
          <view class="neu-secondary-btn button-secondary">
            <text class="button-text">次要按钮</text>
          </view>
        </view>
        <view class="button-row">
          <view class="neu-primary-btn button-small">
            <text class="button-text-small">小按钮</text>
          </view>
          <view class="neu-primary-btn button-large">
            <text class="button-text-large">大按钮</text>
          </view>
        </view>
        <view class="neu-inset-sm button-danger">
          <text class="button-text-danger">危险按钮</text>
        </view>
      </view>
    </view>

    <!-- 8. 文章与段落 Typography -->
    <view class="comp-section">
      <text class="comp-label">8. 文章与段落 Typography</text>
      <view class="neu-card typography-card">
        <text class="forum-h2">标题文本 H2</text>
        <text class="forum-h3">副标题 H3</text>
        <text class="forum-body">这是正文内容。论坛帖子支持富文本格式,包含多种字体大小和样式,为用户提供舒适的阅读体验。</text>
        <text class="forum-caption">这是辅助说明文字,用于补充说明或显示时间戳等次要信息。</text>
      </view>
    </view>

    <!-- 9. 图片 Image -->
    <view class="comp-section">
      <text class="comp-label">9. 图片 Image</text>
      <view class="neu-card image-card">
        <view class="image-placeholder">
          <uv-icon name="photo" :size="40" color="#fff" opacity="0.6"></uv-icon>
        </view>
        <view class="forum-caption center-text">圆角图片示例</view>
      </view>
    </view>

    <!-- 10. 相册 Gallery -->
    <view class="comp-section">
      <text class="comp-label">10. 相册 Gallery</text>
      <view class="gallery-grid">
        <view class="gallery-item" style="background: linear-gradient(135deg, #07c160, #2fe25f);">
          <uv-icon name="photo" :size="20" color="#fff" opacity="0.5"></uv-icon>
        </view>
        <view class="gallery-item" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);">
          <uv-icon name="photo" :size="20" color="#fff" opacity="0.5"></uv-icon>
        </view>
        <view class="gallery-item" style="background: linear-gradient(135deg, #f59e0b, #fcd34d);">
          <uv-icon name="photo" :size="20" color="#fff" opacity="0.5"></uv-icon>
        </view>
        <view class="gallery-item" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);">
          <uv-icon name="photo" :size="20" color="#fff" opacity="0.5"></uv-icon>
        </view>
      </view>
    </view>

    <!-- 11. 表单组件 Form -->
    <view class="comp-section">
      <text class="comp-label">11. 表单组件 Form</text>
      <view class="neu-card form-card">
        <view class="form-item">
          <text class="forum-caption">用户名</text>
          <view class="neu-inset-sm input-wrapper">
            <input type="text" placeholder="请输入用户名" class="form-input" placeholder-class="input-placeholder" />
          </view>
        </view>
        <view class="form-item">
          <text class="forum-caption">留言内容</text>
          <view class="neu-inset-sm textarea-wrapper">
            <textarea placeholder="请输入留言内容..." class="form-textarea" placeholder-class="input-placeholder"></textarea>
          </view>
        </view>
      </view>
    </view>

    <!-- 12. 复选框/单选框/开关 -->
    <view class="comp-section">
      <text class="comp-label">12. 复选框/单选框/开关</text>
      <view class="neu-card checkbox-card">
        <view class="checkbox-item">
          <view class="neu-flat-sm checkbox checked">
            <uv-icon name="checkmark" :size="14" color="#fff"></uv-icon>
          </view>
          <text class="forum-body">记住我</text>
        </view>
        <view class="checkbox-item">
          <view class="neu-flat-sm radio"></view>
          <text class="forum-body">选项 A</text>
        </view>
        <view class="checkbox-item">
          <view class="neu-flat-sm radio checked">
            <view class="radio-dot"></view>
          </view>
          <text class="forum-body">选项 B (选中)</text>
        </view>
        <view class="toggle-item">
          <text class="forum-body">推送通知</text>
          <view class="neu-toggle-track" :class="{ active: toggleNotification }" @tap="toggleNotification = !toggleNotification">
            <view class="neu-toggle-thumb"></view>
          </view>
        </view>
        <view class="toggle-item">
          <text class="forum-body">夜间模式</text>
          <view class="neu-toggle-track" :class="{ active: toggleNight }" @tap="toggleNight = !toggleNight">
            <view class="neu-toggle-thumb"></view>
          </view>
        </view>
      </view>
    </view>

    <!-- 13. 评分 Rating -->
    <view class="comp-section">
      <text class="comp-label">13. 评分 Rating</text>
      <view class="neu-card rating-card">
        <view class="rating-row">
          <uv-icon name="star-fill" :size="22" color="#f59e0b"></uv-icon>
          <uv-icon name="star-fill" :size="22" color="#f59e0b"></uv-icon>
          <uv-icon name="star-fill" :size="22" color="#f59e0b"></uv-icon>
          <uv-icon name="star-fill" :size="22" color="#f59e0b"></uv-icon>
          <uv-icon name="star" :size="22" color="#c8d0e7"></uv-icon>
          <text class="forum-caption">4.0</text>
        </view>
        <view class="rating-row">
          <uv-icon name="star-fill" :size="18" color="#f59e0b"></uv-icon>
          <uv-icon name="star-fill" :size="18" color="#f59e0b"></uv-icon>
          <uv-icon name="star-fill" :size="18" color="#f59e0b"></uv-icon>
          <uv-icon name="star" :size="18" color="#c8d0e7"></uv-icon>
          <uv-icon name="star" :size="18" color="#c8d0e7"></uv-icon>
          <text class="forum-caption">3.0 (小尺寸)</text>
        </view>
      </view>
    </view>

    <!-- 14. 搜索框 Search -->
    <view class="comp-section">
      <text class="comp-label">14. 搜索框 Search</text>
      <view class="neu-inset search-box">
        <uv-icon name="search" :size="16" color="#9baacf"></uv-icon>
        <input type="text" placeholder="搜索帖子、用户、话题..." class="search-input" placeholder-class="input-placeholder" />
      </view>
    </view>

    <!-- 15. 步进器 Stepper -->
    <view class="comp-section">
      <text class="comp-label">15. 步进器 Stepper</text>
      <view class="neu-card stepper-card">
        <view class="neu-flat-sm stepper-btn">
          <uv-icon name="minus" :size="16" color="#9baacf"></uv-icon>
        </view>
        <view class="neu-inset-sm stepper-display">
          <text class="forum-h4">5</text>
        </view>
        <view class="neu-flat-sm stepper-btn primary">
          <uv-icon name="plus" :size="16" color="#fff"></uv-icon>
        </view>
      </view>
    </view>

    <!-- 16. 上传 Upload -->
    <view class="comp-section">
      <text class="comp-label">16. 上传 Upload</text>
      <view class="neu-inset upload-area">
        <z-icon name="upload" :size="32" color="#07c160"></z-icon>
        <text class="forum-body">点击或拖拽上传</text>
        <text class="forum-caption">支持 JPG、PNG 格式</text>
      </view>
    </view>

    <!-- 17. 滑动选择器 Slider -->
    <view class="comp-section">
      <text class="comp-label">17. 滑动选择器 Slider</text>
      <view class="neu-card slider-card">
        <view class="slider-header">
          <text class="forum-caption">字体大小</text>
          <text class="forum-body">60%</text>
        </view>
        <view class="neu-slider-track">
          <view class="neu-slider-fill"></view>
          <view class="neu-slider-thumb"></view>
        </view>
      </view>
    </view>

    <!-- 18. 列表 List -->
    <view class="comp-section">
      <text class="comp-label">18. 列表 List</text>
      <view class="list-container">
        <view class="neu-card list-item">
          <view class="neu-flat-sm list-avatar" style="background: linear-gradient(135deg, #07c160, #2fe25f);">
            <uv-icon name="account" :size="16" color="#fff"></uv-icon>
          </view>
          <view class="list-content">
            <text class="forum-body">科技爱好者小王</text>
            <text class="forum-caption">最新发布了关于 AI 的帖子</text>
          </view>
          <uv-icon name="arrow-right" :size="16" color="#bec8e4"></uv-icon>
        </view>
        <view class="neu-card list-item">
          <view class="neu-flat-sm list-avatar" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);">
            <uv-icon name="account" :size="16" color="#fff"></uv-icon>
          </view>
          <view class="list-content">
            <text class="forum-body">设计师小李</text>
            <text class="forum-caption">回复了你的评论</text>
          </view>
          <uv-icon name="arrow-right" :size="16" color="#bec8e4"></uv-icon>
        </view>
      </view>
    </view>

    <!-- 19. 标签 Tags/Chips -->
    <view class="comp-section">
      <text class="comp-label">19. 标签 Tags/Chips</text>
      <view class="tags-container">
        <view class="neu-flat-sm tag" style="color: #07c160;">
          <text>热门</text>
        </view>
        <view class="neu-flat-sm tag" style="color: #6d5dfc;">
          <text>科技</text>
        </view>
        <view class="neu-flat-sm tag" style="color: #f59e0b;">
          <text>美食</text>
        </view>
        <view class="neu-flat-sm tag" style="color: #ef4444;">
          <text>紧急</text>
        </view>
        <view class="neu-flat-sm tag" style="color: #9baacf;">
          <text>日常</text>
        </view>
        <view class="neu-flat-sm tag primary" style="background: #07c160; color: #fff;">
          <text>精选</text>
        </view>
      </view>
    </view>

    <!-- 20. 数字角标 Badge -->
    <view class="comp-section">
      <text class="comp-label">20. 数字角标 Badge</text>
      <view class="neu-card badge-grid">
        <view class="badge-item">
          <view class="badge-wrapper">
            <uv-icon name="home" :size="24" color="#9baacf"></uv-icon>
            <view class="badge-dot">
              <text>3</text>
            </view>
          </view>
        </view>
        <view class="badge-item">
          <view class="badge-wrapper">
            <uv-icon name="chat" :size="24" color="#9baacf"></uv-icon>
            <view class="badge-dot">
              <text>12</text>
            </view>
          </view>
        </view>
        <view class="badge-item">
          <view class="badge-wrapper">
            <uv-icon name="bell" :size="24" color="#9baacf"></uv-icon>
            <view class="badge-dot dot"></view>
          </view>
        </view>
        <view class="badge-item">
          <view class="badge-wrapper">
            <uv-icon name="shopping-cart" :size="24" color="#9baacf"></uv-icon>
            <view class="badge-dot">
              <text>99</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- 21. 线形进度条 Progress Bar -->
    <view class="comp-section">
      <text class="comp-label">21. 线形进度条 Progress Bar</text>
      <view class="neu-card progress-card">
        <view class="progress-item">
          <view class="progress-header">
            <text class="forum-caption">资料完善度</text>
            <text class="forum-caption">65%</text>
          </view>
          <view class="neu-progress-track">
            <view class="neu-progress-fill" style="width: 65%;"></view>
          </view>
        </view>
        <view class="progress-item">
          <view class="progress-header">
            <text class="forum-caption">上传进度</text>
            <text class="forum-caption">30%</text>
          </view>
          <view class="neu-progress-track">
            <view class="neu-progress-fill" style="width: 30%;"></view>
          </view>
        </view>
      </view>
    </view>

    <!-- 22. 加载动画 Loading -->
    <view class="comp-section">
      <text class="comp-label">22. 加载动画 Loading</text>
      <view class="neu-card loading-card">
        <view class="neu-spinner"></view>
        <text class="forum-caption">加载中...</text>
      </view>
    </view>

    <!-- 23. 内容为空 Empty State -->
    <view class="comp-section">
      <text class="comp-label">23. 内容为空 Empty State</text>
      <view class="neu-card empty-card">
        <view class="neu-inset empty-icon"></view>
        <text class="forum-body">暂无内容</text>
        <text class="forum-caption">快去发布你的第一条帖子吧</text>
            <view class="neu-primary-btn empty-button">
              <text class="button-text-small">去发布</text>
            </view>
      </view>
    </view>

    <!-- 24. Alert/Toast/Notify -->
    <view class="comp-section">
      <text class="comp-label">24. Alert / Toast / Notify</text>
      <view class="toast-container">
        <view class="neu-toast">
          <uv-icon name="checkmark-circle" :size="18" color="#07c160"></uv-icon>
          <text class="forum-body">操作成功</text>
        </view>
        <view class="neu-toast">
          <uv-icon name="warning" :size="18" color="#f59e0b"></uv-icon>
          <text class="forum-body">请注意,此操作不可撤销</text>
        </view>
        <view class="neu-toast">
          <uv-icon name="close-circle" :size="18" color="#ef4444"></uv-icon>
          <text class="forum-body">网络连接失败,请重试</text>
        </view>
        <view class="neu-toast">
          <uv-icon name="error-circle" :size="18" color="#6d5dfc"></uv-icon>
          <text class="forum-body">系统将于今晚 22:00 维护</text>
        </view>
      </view>
    </view>

    <!-- 25. Modal 模态框 -->
    <view class="comp-section">
      <text class="comp-label">25. Modal 模态框</text>
      <view class="modal-overlay">
        <view class="neu-card modal-card">
          <uv-icon name="error-circle" :size="36" color="#f59e0b"></uv-icon>
          <text class="forum-h4 center-text">确认删除</text>
          <text class="forum-body center-text">删除后将无法恢复,是否继续?</text>
          <view class="modal-buttons">
            <view class="neu-secondary-btn modal-btn">
              <text class="button-text-small">取消</text>
            </view>
            <view class="neu-primary-btn modal-btn danger">
              <text class="button-text-small">删除</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- 26. Cell 单元格 -->
    <view class="comp-section">
      <text class="comp-label">26. Cell 单元格</text>
      <view class="neu-card cell-list">
        <view class="cell-item">
          <uv-icon name="account" :size="20" color="#07c160"></uv-icon>
          <text class="forum-body">个人资料</text>
          <uv-icon name="arrow-right" :size="16" color="#bec8e4"></uv-icon>
        </view>
        <view class="cell-item">
          <uv-icon name="star" :size="20" color="#6d5dfc"></uv-icon>
          <text class="forum-body">我的收藏</text>
          <uv-icon name="arrow-right" :size="16" color="#bec8e4"></uv-icon>
        </view>
        <view class="cell-item">
          <uv-icon name="calendar" :size="20" color="#f59e0b"></uv-icon>
          <text class="forum-body">隐私设置</text>
          <uv-icon name="arrow-right" :size="16" color="#bec8e4"></uv-icon>
        </view>
        <view class="cell-item last">
          <uv-icon name="question-circle" :size="20" color="#9baacf"></uv-icon>
          <text class="forum-body">帮助与反馈</text>
          <uv-icon name="arrow-right" :size="16" color="#bec8e4"></uv-icon>
        </view>
      </view>
    </view>

    <!-- 27. 折叠面板 Accordion -->
    <view class="comp-section">
      <text class="comp-label">27. 折叠面板 Accordion</text>
      <view class="accordion-container">
        <view class="neu-card accordion-item">
          <view class="accordion-header" @tap="accordionOpen = accordionOpen === 0 ? -1 : 0">
            <text class="forum-body">什么是拟物设计?</text>
            <uv-icon :name="accordionOpen === 0 ? 'arrow-up' : 'arrow-down'" :size="16" color="#9baacf"></uv-icon>
          </view>
          <view class="accordion-body" v-show="accordionOpen === 0">
            <text class="forum-caption">拟物设计通过柔和的阴影和高光模拟真实物体的凸起和凹陷,营造具有触感的界面效果。</text>
          </view>
        </view>
        <view class="neu-card accordion-item">
          <view class="accordion-header" @tap="accordionOpen = accordionOpen === 1 ? -1 : 1">
            <text class="forum-body">如何切换主题?</text>
            <uv-icon :name="accordionOpen === 1 ? 'arrow-up' : 'arrow-down'" :size="16" color="#9baacf"></uv-icon>
          </view>
          <view class="accordion-body" v-show="accordionOpen === 1">
            <text class="forum-caption">前往设置页面,在显示选项中可以选择不同的主题风格。</text>
          </view>
        </view>
        <view class="neu-card accordion-item">
          <view class="accordion-header" @tap="accordionOpen = accordionOpen === 2 ? -1 : 2">
            <text class="forum-body">支持哪些设备?</text>
            <uv-icon :name="accordionOpen === 2 ? 'arrow-up' : 'arrow-down'" :size="16" color="#9baacf"></uv-icon>
          </view>
          <view class="accordion-body" v-show="accordionOpen === 2">
            <text class="forum-caption">目前支持 iOS 和 Android 平台,后续将适配更多设备。</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 28. 宫格布局 Grid Layout -->
    <view class="comp-section">
      <text class="comp-label">28. 宫格布局 Grid Layout</text>
      <view class="neu-card grid-layout">
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #07c160, #2fe25f);">
            <uv-icon name="scan" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">扫一扫</text>
        </view>
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);">
            <uv-icon name="red-packet" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">钱包</text>
        </view>
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #f59e0b, #fcd34d);">
            <uv-icon name="gift" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">福利</text>
        </view>
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #ef4444, #fca5a5);">
            <uv-icon name="heart" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">公益</text>
        </view>
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);">
            <uv-icon name="empty-address" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">附近</text>
        </view>
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #ec4899, #f9a8d4);">
            <uv-icon name="bag" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">商城</text>
        </view>
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #06b6d4, #67e8f9);">
            <uv-icon name="empty-favor" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">游戏</text>
        </view>
        <view class="grid-item">
          <view class="neu-flat-sm grid-icon" style="background: linear-gradient(135deg, #8b5cf6, #c4b5fd);">
            <uv-icon name="grid" :size="20" color="#fff"></uv-icon>
          </view>
          <text class="grid-label">更多</text>
        </view>
      </view>
    </view>

    <!-- 29. 底部导航栏 Bottom Nav -->
    <view class="comp-section">
      <text class="comp-label">29. 底部导航栏 Bottom Nav</text>
      <view class="neu-card bottom-nav-demo">
        <view class="nav-items">
          <view class="nav-item active">
            <uv-icon name="home" :size="22" color="#07c160"></uv-icon>
            <text class="nav-label active">首页</text>
          </view>
          <view class="nav-item">
            <uv-icon name="eye" :size="22" color="#9baacf"></uv-icon>
            <text class="nav-label">发现</text>
          </view>
          <view class="nav-item center">
            <view class="neu-fab">
              <uv-icon name="plus" :size="24" color="#fff"></uv-icon>
            </view>
          </view>
          <view class="nav-item">
            <uv-icon name="chat" :size="22" color="#9baacf"></uv-icon>
            <text class="nav-label">消息</text>
          </view>
          <view class="nav-item">
            <uv-icon name="account" :size="22" color="#9baacf"></uv-icon>
            <text class="nav-label">我的</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 30. 操作菜单 Action Sheet -->
    <view class="comp-section">
      <text class="comp-label">30. 操作菜单 Action Sheet</text>
      <view class="modal-overlay">
        <view class="neu-card action-sheet">
          <view class="action-item">
            <text class="forum-body">拍照</text>
          </view>
          <view class="action-item">
            <text class="forum-body">从相册选择</text>
          </view>
          <view class="action-item last">
            <text class="forum-body">保存到本地</text>
          </view>
        </view>
        <view class="neu-card action-sheet cancel">
          <view class="action-item">
            <text class="forum-caption">取消</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 31. Tabs 标签选项卡 -->
    <view class="comp-section">
      <text class="comp-label">31. Tabs 标签选项卡</text>
      <view class="neu-card tabs-bar">
        <view class="tab" :class="{ active: activeTab === 0 }" @tap="activeTab = 0">
          <text>推荐</text>
        </view>
        <view class="tab" :class="{ active: activeTab === 1 }" @tap="activeTab = 1">
          <text>关注</text>
        </view>
        <view class="tab" :class="{ active: activeTab === 2 }" @tap="activeTab = 2">
          <text>热榜</text>
        </view>
        <view class="tab" :class="{ active: activeTab === 3 }" @tap="activeTab = 3">
          <text>视频</text>
        </view>
      </view>
    </view>

    <!-- 32. 步骤条 Steps -->
    <view class="comp-section">
      <text class="comp-label">32. 步骤条 Steps</text>
      <view class="neu-card steps-card">
        <view class="steps-row">
          <view class="step">
            <view class="neu-flat-sm step-icon done">
              <uv-icon name="checkmark" :size="14" color="#fff"></uv-icon>
            </view>
            <text class="forum-caption">提交</text>
          </view>
          <view class="step-line done"></view>
          <view class="step">
            <view class="neu-flat-sm step-icon current">
              <text class="step-number">2</text>
            </view>
            <text class="forum-caption primary">审核</text>
          </view>
          <view class="step-line"></view>
          <view class="step">
            <view class="neu-inset-sm step-icon">
              <text class="step-number">3</text>
            </view>
            <text class="forum-caption">完成</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 33. 倒计时 Countdown -->
    <view class="comp-section">
      <text class="comp-label">33. 倒计时 Countdown</text>
      <view class="neu-card countdown-card">
        <text class="forum-caption">距活动结束还剩</text>
        <view class="countdown-row">
          <view class="neu-inset countdown-box" style="display: flex; justify-content: center; align-items: center;">
            <text class="forum-h3">02</text>
          </view>
          <text class="forum-h3">:</text>
          <view class="neu-inset countdown-box" style="display: flex; justify-content: center; align-items: center;">
            <text class="forum-h3">15</text>
          </view>
          <text class="forum-h3">:</text>
          <view class="neu-inset countdown-box" style="display: flex; justify-content: center; align-items: center;">
            <text class="forum-h3">38</text>
          </view>
        </view>
        <view class="countdown-labels">
          <view class="forum-caption" style="display: flex; justify-content: center; align-items: center;">时</view>
          <text class="forum-caption">分</text>
          <text class="forum-caption">秒</text>
        </view>
      </view>
    </view>

    <!-- 34. 头像 Avatar -->
    <view class="comp-section">
      <text class="comp-label">34. 头像 Avatar</text>
      <view class="neu-card avatar-card">
        <view class="avatar-main">
          <view class="avatar-wrapper">
            <view class="neu-flat-sm avatar-large" style="background: linear-gradient(135deg, #07c160, #2fe25f);">
              <text class="avatar-text-large">K</text>
            </view>
            <view class="online-dot"></view>
          </view>
          <view class="avatar-info">
            <text class="forum-body bold">Kira Zhang</text>
            <text class="forum-caption">在线</text>
          </view>
        </view>
        <view class="avatar-row">
          <view class="avatar-wrapper small">
            <view class="neu-flat-sm avatar-small" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);">
              <text class="avatar-text-small">A</text>
            </view>
            <view class="offline-dot"></view>
          </view>
          <view class="avatar-wrapper small">
            <view class="neu-flat-sm avatar-small" style="background: linear-gradient(135deg, #f59e0b, #fcd34d);">
              <text class="avatar-text-small">B</text>
            </view>
            <view class="busy-dot"></view>
          </view>
          <view class="avatar-wrapper small">
            <view class="neu-flat-sm avatar-small" style="background: linear-gradient(135deg, #6d5dfc, #8abdff);">
              <text class="avatar-text-small">C</text>
            </view>
            <view class="online-dot small"></view>
          </view>
          <view class="neu-inset-sm avatar-add">
            <uv-icon name="plus" :size="18" color="#9baacf"></uv-icon>
          </view>
        </view>
      </view>
    </view>

    <!-- 35. 返回顶部 Back to Top -->
    <view class="comp-section">
      <text class="comp-label">35. 返回顶部 Back to Top</text>
      <view class="back-to-top">
        <view class="neu-fab">
          <uv-icon name="arrow-up" :size="22" color="#fff"></uv-icon>
        </view>
      </view>
    </view>

    <!-- 36. 自定义导航栏 Custom Navbar -->
    <view class="comp-section">
      <text class="comp-label">36. 自定义导航栏 Custom Navbar</text>
      <view class="neu-card custom-navbar">
        <view class="navbar-top">
          <view class="navbar-left">
            <uv-icon name="arrow-left" :size="22" color="#2d3748"></uv-icon>
          </view>
          <text class="forum-h4 center-text">帖子详情</text>
          <view class="navbar-right">
            <uv-icon name="share" :size="20" color="#2d3748"></uv-icon>
          </view>
        </view>
        <view class="navbar-divider"></view>
        <view class="navbar-actions">
          <view class="action-item">
            <uv-icon name="chat" :size="18" color="#9baacf"></uv-icon>
            <text class="action-label">128</text>
          </view>
          <view class="action-item">
            <uv-icon name="heart" :size="18" color="#ef4444"></uv-icon>
            <text class="action-label error">256</text>
          </view>
          <view class="action-item">
            <uv-icon name="star" :size="18" color="#f59e0b"></uv-icon>
            <text class="action-label warning">收藏</text>
          </view>
          <view class="action-item">
            <uv-icon name="minus-circle" :size="18" color="#9baacf"></uv-icon>
            <text class="action-label">举报</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 底部占位 -->
    <view style="height: 80px;"></view>
  </view>
</template>

<script setup>
import { ref } from 'vue';
import { onLoad, onShow } from "@dcloudio/uni-app";
// import { useGlobalStore } from '@/stores/index';
// const globalStore = useGlobalStore();

// Toggle state
const toggleNotification = ref(true);
const toggleNight = ref(false);

// Accordion state
const accordionOpen = ref(0);

// Tab state
const activeTab = ref(0);

let checked = ref(true);

onShow(() => {
  // globalStore.tab_bar_current = 4;
  uni.hideTabBar();
});
</script>

<style lang="scss">
:root {
  --primary-light: #2fe25f;
  --primary: #07c160;
  --primary-dark: #0eb805;
  --secondary-light: #8abdff;
  --secondary: #6d5dfc;
  --secondary-dark: #5b0eeb;
  --white: #FFFFFF;
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --neu-shadow-out: 0.6rem 0.6rem 1.2rem var(--greyLight-2), -0.4rem -0.4rem 1rem var(--white);
  --neu-shadow-in: inset 0.4rem 0.4rem 0.8rem var(--greyLight-2), inset -0.4rem -0.4rem 0.8rem var(--white);
  --neu-shadow-sm: 0.2rem 0.2rem 0.4rem var(--greyLight-2), -0.15rem -0.15rem 0.3rem var(--white);
  --neu-shadow-sm-in: inset 0.15rem 0.15rem 0.3rem var(--greyLight-2), inset -0.15rem -0.15rem 0.3rem var(--white);
  --forum-background: var(--greyLight-1);
  --forum-foreground: #2d3748;
  --forum-card: var(--white);
  --forum-primary: var(--primary);
  --forum-primary-foreground: var(--white);
  --forum-muted: var(--greyLight-2);
  --forum-muted-foreground: var(--greyDark);
  --forum-border: var(--greyLight-2);
  --forum-radius-sm: 8px;
  --forum-radius-md: 12px;
  --forum-radius-lg: 16px;
  --forum-radius-full: 9999px;
  --text-xs: 0.6875rem;
  --text-sm: 0.75rem;
  --text-base: 0.875rem;
  --text-lg: 1rem;
  --text-xl: 1.125rem;
  --text-2xl: 1.25rem;
  --text-3xl: 1.5rem;
  --text-4xl: 2rem;
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 12px;
  --spacing-lg: 16px;
  --spacing-xl: 24px;
  --spacing-2xl: 32px;
  --surface-raised: var(--greyLight-1);
  --state-success: var(--primary);
  --state-warning: #f59e0b;
  --state-error: #ef4444;
  --state-info: var(--secondary);
  --transition-fast: 0.2s ease;
  --transition-normal: 0.3s ease;
  --font-body: "Poppins", "PingFang SC", "Microsoft YaHei", sans-serif;
  --font-display: "Poppins", "PingFang SC", "Microsoft YaHei", sans-serif;
}

page {
  background: var(--greyLight-1);
}

.ui-components-page {
  min-height: 100vh;
  background: var(--forum-background);
  padding-bottom: 120rpx;
}

/* Section styles */
.comp-section {
  padding: 24rpx 32rpx;
}

.comp-label {
  font-size: 24rpx;
  font-weight: 600;
  color: var(--forum-muted-foreground);
  letter-spacing: 0.04em;
  text-transform: uppercase;
  margin-bottom: 24rpx;
  padding-left: 8rpx;
  display: block;
}

/* Neumorphic base classes */
.neu-card {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-out);
  border-radius: var(--forum-radius-md);
  padding: 32rpx;
}

.neu-inset {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-in);
  border-radius: var(--forum-radius-md);
}

.neu-flat-sm {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-sm);
  border-radius: var(--forum-radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
}

.neu-inset-sm {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-sm-in);
  border-radius: var(--forum-radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
}

.neu-primary-btn {
  background: linear-gradient(330deg, var(--primary-dark) 0%, var(--primary) 50%, var(--primary-light) 100%);
  box-shadow: var(--neu-shadow-sm);
  border-radius: var(--forum-radius-lg);
  color: var(--forum-primary-foreground);
  display: flex;
  align-items: center;
  justify-content: center;
}

.neu-secondary-btn {
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-out);
  border-radius: var(--forum-radius-lg);
  color: var(--forum-muted-foreground);
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Typography classes */
.forum-h3 {
  font-size: 32rpx;
  font-weight: 600;
  color: var(--forum-foreground);
}

.forum-h4 {
  font-size: 28rpx;
  font-weight: 600;
  color: var(--forum-foreground);
}

.forum-body {
  font-size: 28rpx;
  color: var(--forum-foreground);
  line-height: 1.6;
}

.forum-caption {
  font-size: 24rpx;
  color: var(--forum-muted-foreground);
  line-height: 1.5;
}

/* Header */
.header-box {
  display: flex;
  align-items: center;
  margin-bottom: 16rpx;
}

.header-icon {
  width: 80rpx;
  height: 80rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 24rpx;
  background: linear-gradient(330deg, var(--primary-dark), var(--primary), var(--primary-light));
  box-shadow: var(--neu-shadow-sm);
  margin-right: 24rpx;
}

.header-text {
  display: flex;
  flex-direction: column;
}

/* Skeleton */
.skeleton-card {
  display: flex;
  flex-direction: column;
}

.skeleton-header {
  display: flex;
  align-items: center;
  margin-bottom: 24rpx;
}

.skeleton-bar {
  background: var(--greyLight-2);
  border-radius: var(--forum-radius-sm);
  box-shadow: var(--neu-shadow-sm-in);
  animation: skeleton-pulse 1.8s ease-in-out infinite;
}

.skeleton-avatar {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  flex-shrink: 0;
  margin-right: 24rpx;
}

.skeleton-info {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.skeleton-title {
  width: 55%;
  height: 28rpx;
  margin-bottom: 16rpx;
}

.skeleton-subtitle {
  width: 35%;
  height: 20rpx;
}

.skeleton-line {
  width: 100%;
  height: 24rpx;
  margin-bottom: 16rpx;
}

.skeleton-line.short {
  width: 80%;
}

.skeleton-line.shorter {
  width: 60%;
}

@keyframes skeleton-pulse {
  0%, 100% { opacity: 0.4; }
  50% { opacity: 0.7; }
}

/* Calendar */
.calendar-card {
  padding: 32rpx;
}

.calendar-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 24rpx;
}

.calendar-weekdays {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  text-align: center;
  margin-bottom: 16rpx;
}

.weekday {
  font-size: 20rpx;
}

.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  justify-items: center;
}

.cal-cell {
  width: 72rpx;
  height: 64rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24rpx;
  border-radius: var(--forum-radius-sm);
}

.cal-cell.today {
  background: linear-gradient(330deg, var(--primary-dark), var(--primary), var(--primary-light));
  color: var(--white);
  box-shadow: var(--neu-shadow-sm);
}

.cal-cell.other-month {
  color: var(--greyLight-3);
}

/* Dropdown */
.dropdown-row {
  display: flex;
}

.dropdown-item {
  flex: 1;
  padding: 16rpx 24rpx;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-right: 16rpx;
}

.dropdown-item:last-child {
  margin-right: 0;
}

/* Vertical Tabs */
.vertical-tabs {
  display: flex;
  min-height: 280rpx;
  padding: 0;
  overflow: hidden;
}

.tabs-sidebar {
  width: 160rpx;
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-sm);
  display: flex;
  flex-direction: column;
}

.tab-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 24rpx 0;
  color: var(--forum-muted-foreground);
}

.tab-item.active {
  background: linear-gradient(330deg, var(--primary-dark), var(--primary), var(--primary-light));
  color: var(--white);
  border-radius: 0 var(--forum-radius-sm) var(--forum-radius-sm) 0;
}

.tab-text {
  font-size: 20rpx;
  margin-top: 8rpx;
}

.tabs-content {
  flex: 1;
  padding: 24rpx;
}

.content-items {
  display: flex;
  flex-direction: column;
  margin-top: 16rpx;
}

.content-item {
  padding: 16rpx;
  margin-bottom: 16rpx;
}

.caption-text {
  font-size: 24rpx;
  color: var(--forum-muted-foreground);
}

/* Waterfall */
.waterfall {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20rpx;
}

.waterfall-item {
  margin-bottom: 20rpx;
}

.waterfall-card {
  padding: 0;
  overflow: hidden;
}

.waterfall-image {
  width: 100%;
  height: 200rpx;
}

.waterfall-image.tall {
  height: 280rpx;
}

.waterfall-image.short {
  height: 160rpx;
}

.waterfall-image.medium {
  height: 240rpx;
}

.waterfall-content {
  padding: 16rpx;
}

/* Icons */
.icon-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 24rpx;
}

.icon-item {
  padding: 24rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.icon-label {
  font-size: 20rpx;
  color: var(--forum-muted-foreground);
  margin-top: 8rpx;
}

/* Buttons */
.button-group {
  display: flex;
  flex-direction: column;
}

.button-row {
  display: flex;
  margin-bottom: 24rpx;
}

.button-primary,
.button-secondary {
  flex: 1;
  padding: 24rpx 0;
  margin-right: 24rpx;
}

.button-primary:last-child,
.button-secondary:last-child {
  margin-right: 0;
}

.button-small {
  flex: 1;
  padding: 16rpx 0;
  margin-right: 24rpx;
}

.button-large {
  flex: 1;
  padding: 32rpx 0;
}

.button-text {
  font-size: 28rpx;
  font-weight: 600;
}

.button-text-small {
  font-size: 24rpx;
  font-weight: 600;
}

.button-text-large {
  font-size: 32rpx;
  font-weight: 600;
}

.button-danger {
  padding: 16rpx 0;
  text-align: center;
  color: var(--state-error);
}

.button-text-danger {
  font-size: 24rpx;
  color: var(--state-error);
}

/* Typography */
.typography-card {
  display: flex;
  flex-direction: column;
}

.typography-card .forum-h2,
.typography-card .forum-h3,
.typography-card .forum-body,
.typography-card .forum-caption {
  margin-bottom: 24rpx;
}

/* Image */
.image-card {
  padding: 12rpx;
  overflow: hidden;
}

.image-placeholder {
  width: 100%;
  height: 360rpx;
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  border-radius: var(--forum-radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
}

.center-text {
  text-align: center;
  margin-top: 16rpx;
}

/* Gallery */
.gallery-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 16rpx;
}

.gallery-item {
  height: 180rpx;
  border-radius: var(--forum-radius-sm);
  box-shadow: var(--neu-shadow-sm);
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Form */
.form-card {
  display: flex;
  flex-direction: column;
}

.form-item {
  margin-bottom: 24rpx;
}

.form-item:last-child {
  margin-bottom: 0;
}

.input-wrapper,
.textarea-wrapper {
  padding: 16rpx 24rpx;
  margin-top: 8rpx;
}

.textarea-wrapper {
  min-height: 144rpx;
}

.form-input,
.form-textarea {
  width: 100%;
  background: transparent;
  border: none;
  outline: none;
  font-size: 24rpx;
  color: var(--forum-foreground);
  font-family: var(--font-body);
}

.form-textarea {
  height: 112rpx;
  resize: none;
}

.input-placeholder {
  color: var(--greyDark);
}

/* Checkbox */
.checkbox-card {
  display: flex;
  flex-direction: column;
}

.checkbox-item,
.toggle-item {
  display: flex;
  align-items: center;
  margin-bottom: 32rpx;
}

.checkbox-item:last-child,
.toggle-item:last-child {
  margin-bottom: 0;
}

.checkbox,
.radio {
  width: 44rpx;
  height: 44rpx;
  margin-right: 24rpx;
}

.checkbox.checked {
  background: var(--primary);
}

.radio.checked {
  background: var(--primary);
}

.radio-dot {
  width: 16rpx;
  height: 16rpx;
  background: var(--white);
  border-radius: 50%;
}

.toggle-item {
  justify-content: space-between;
}

.neu-toggle-track {
  width: 88rpx;
  height: 48rpx;
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-in);
  border-radius: 24rpx;
  position: relative;
  cursor: pointer;
  transition: background var(--transition-fast);
}

.neu-toggle-thumb {
  width: 36rpx;
  height: 36rpx;
  background: var(--greyLight-2);
  box-shadow: var(--neu-shadow-sm);
  border-radius: 50%;
  position: absolute;
  top: 6rpx;
  left: 6rpx;
  transition: all var(--transition-fast);
}

.neu-toggle-track.active {
  background: var(--primary);
}

.neu-toggle-track.active .neu-toggle-thumb {
  left: 46rpx;
  background: var(--white);
}

/* Rating */
.rating-card {
  display: flex;
  flex-direction: column;
}

.rating-row {
  display: flex;
  align-items: center;
  margin-bottom: 24rpx;
}

.rating-row:last-child {
  margin-bottom: 0;
}

.rating-row .forum-caption {
  margin-left: 8rpx;
}

/* Search */
.search-box {
  padding: 16rpx 24rpx;
  display: flex;
  align-items: center;
}

.search-input {
  flex: 1;
  background: transparent;
  border: none;
  outline: none;
  font-size: 24rpx;
  color: var(--forum-foreground);
  font-family: var(--font-body);
  margin-left: 16rpx;
}

/* Stepper */
.stepper-card {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 32rpx;
}

.stepper-btn {
  width: 72rpx;
  height: 72rpx;
}

.stepper-btn.primary {
  background: var(--primary);
}

.stepper-display {
  width: 112rpx;
  height: 72rpx;
  margin: 0 32rpx;
}

/* Upload */
.upload-area {
  padding: 96rpx 32rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: 4rpx dashed var(--greyLight-3);
  text-align: center;
}

.upload-area .forum-body {
  margin-top: 16rpx;
}

.upload-area .forum-caption {
  margin-top: 8rpx;
}

/* Slider */
.slider-card {
  padding: 32rpx;
}

.slider-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 16rpx;
}

.neu-slider-track {
  width: 100%;
  height: 16rpx;
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-in);
  border-radius: 8rpx;
  position: relative;
}

.neu-slider-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--primary-dark), var(--primary));
  border-radius: 8rpx;
  width: 60%;
}

.neu-slider-thumb {
  width: 44rpx;
  height: 44rpx;
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-out);
  border-radius: 50%;
  position: absolute;
  top: 50%;
  left: 60%;
  transform: translate(-50%, -50%);
}

/* List */
.list-container {
  display: flex;
  flex-direction: column;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 24rpx 32rpx;
  margin-bottom: 16rpx;
}

.list-avatar {
  width: 72rpx;
  height: 72rpx;
  border-radius: 50%;
  flex-shrink: 0;
  margin-right: 24rpx;
}

.list-content {
  flex: 1;
  min-width: 0;
  display: flex;
  flex-direction: column;
}

.list-content .forum-body {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.list-content .forum-caption {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-top: 4rpx;
}

/* Tags */
.tags-container {
  display: flex;
  flex-wrap: wrap;
}

.tag {
  padding: 8rpx 24rpx;
  margin-right: 16rpx;
  margin-bottom: 16rpx;
  font-size: 24rpx;
}

.tag.primary {
  background: var(--primary);
}

/* Badge */
.badge-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  padding: 32rpx;
}

.badge-item {
  display: flex;
  align-items: center;
  justify-content: center;
}

.badge-wrapper {
  position: relative;
}

.badge-dot {
  position: absolute;
  top: -14rpx;
  right: -26rpx;
  min-width: 32rpx;
  height: 32rpx;
  background: var(--state-error);
  color: var(--white);
  font-size: 20rpx;
  font-weight: 700;
  border-radius: 16rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 8rpx;
  box-shadow: var(--neu-shadow-sm);
}

.badge-dot.dot {
    top: -8rpx;
    right: -8rpx;
  min-width: 16rpx;
  height: 16rpx;
  padding: 0;
}

/* Progress */
.progress-card {
  display: flex;
  flex-direction: column;
}

.progress-item {
  margin-bottom: 24rpx;
}

.progress-item:last-child {
  margin-bottom: 0;
}

.progress-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8rpx;
}

.neu-progress-track {
  width: 100%;
  height: 16rpx;
  background: var(--surface-raised);
  box-shadow: var(--neu-shadow-in);
  border-radius: 8rpx;
  overflow: hidden;
}

.neu-progress-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--primary-dark), var(--primary-light));
  border-radius: 8rpx;
}

/* Loading */
.loading-card {
  padding: 48rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.neu-spinner {
  width: 72rpx;
  height: 72rpx;
  border: 6rpx solid var(--greyLight-2);
  border-top-color: var(--primary);
  border-radius: 50%;
  animation: spin 0.9s linear infinite;
  box-shadow: var(--neu-shadow-sm);
  margin-right: 24rpx;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Empty */
.empty-card {
  padding: 64rpx 32rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.empty-icon {
  width: 128rpx;
  height: 128rpx;
  border-radius: 50%;
  margin-bottom: 24rpx;
}

.empty-card .forum-body {
  margin-bottom: 16rpx;
}

.empty-button {
  margin-top: 24rpx;
  padding: 16rpx 40rpx;
}

/* Toast */
.toast-container {
  display: flex;
  flex-direction: column;
}

.neu-toast {
  padding: 20rpx 28rpx;
  border-radius: var(--forum-radius-sm);
  box-shadow: var(--neu-shadow-out);
  display: flex;
  align-items: center;
  margin-bottom: 16rpx;
  background: var(--surface-raised);
}

.neu-toast:last-child {
  margin-bottom: 0;
}

.neu-toast .forum-body {
  flex: 1;
  margin-left: 16rpx;
  font-size: 24rpx;
}

/* Modal */
.modal-overlay {
  background: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(4rpx);
  border-radius: var(--forum-radius-lg);
  padding: 48rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.modal-card {
  max-width: 600rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40rpx;
}

.modal-card .forum-h4 {
  margin-top: 24rpx;
}

.modal-card .forum-body {
  margin-top: 16rpx;
  font-size: 24rpx;
}

.modal-buttons {
  display: flex;
  width: 100%;
  margin-top: 32rpx;
}

.modal-btn {
  flex: 1;
  padding: 16rpx 0;
  margin-right: 24rpx;
}

.modal-btn:last-child {
  margin-right: 0;
}

.modal-btn.danger {
  background: var(--state-error);
}

/* Cell */
.cell-list {
  padding: 0;
  overflow: hidden;
}

.cell-item {
  display: flex;
  align-items: center;
  padding: 24rpx 32rpx;
  box-shadow: inset 0 -2rpx 0 var(--greyLight-2);
}

.cell-item.last {
  box-shadow: none;
}

.cell-item .forum-body {
  flex: 1;
  margin: 0 24rpx;
  font-size: 24rpx;
}

/* Accordion */
.accordion-container {
  display: flex;
  flex-direction: column;
}

.accordion-item {
  margin-bottom: 16rpx;
  padding: 0;
  overflow: hidden;
}

.accordion-header {
  padding: 24rpx 32rpx;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.accordion-header .forum-body {
  font-size: 24rpx;
}

.accordion-body {
  padding: 0 32rpx 24rpx;
}

/* Grid Layout */
.grid-layout {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 24rpx;
  padding: 32rpx;
}

.grid-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.grid-icon {
  width: 80rpx;
  height: 80rpx;
  border-radius: var(--forum-radius-sm);
  margin-bottom: 8rpx;
}

.grid-label {
  font-size: 20rpx;
  color: var(--forum-muted-foreground);
}

/* Bottom Nav Demo */
.bottom-nav-demo {
  padding: 24rpx;
}

.nav-items {
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.nav-item.center {
  margin-top: -32rpx;
}

.nav-label {
  font-size: 20rpx;
  color: var(--forum-muted-foreground);
  margin-top: 8rpx;
}

.nav-label.active {
  color: var(--primary);
  font-weight: 600;
}

.neu-fab {
  width: 96rpx;
  height: 96rpx;
  background: linear-gradient(330deg, var(--primary-dark), var(--primary), var(--primary-light));
  box-shadow: var(--neu-shadow-sm);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Action Sheet */
.action-sheet {
  max-width: 600rpx;
  width: 100%;
  padding: 0;
  overflow: hidden;
  margin-bottom: 16rpx;
}

.action-sheet.cancel {
  margin-bottom: 0;
}

.action-item {
  padding: 24rpx 32rpx;
  text-align: center;
  box-shadow: inset 0 -2rpx 0 var(--greyLight-2);
}

.action-item.last {
  box-shadow: none;
}

/* Tabs Bar */
.tabs-bar {
  padding: 8rpx;
  display: flex;
}

.tab {
  flex: 1;
  padding: 16rpx 0;
  text-align: center;
  font-size: 24rpx;
  color: var(--forum-muted-foreground);
  border-radius: var(--forum-radius-sm);
}

.tab.active {
  background: linear-gradient(330deg, var(--primary-dark), var(--primary), var(--primary-light));
  color: var(--white);
  font-weight: 600;
}

/* Steps */
.steps-card {
  padding: 32rpx;
}

.steps-row {
  display: flex;
  align-items: flex-start;
}

.step {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80rpx;
}

.step-icon {
  width: 56rpx;
  height: 56rpx;
  border-radius: 50%;
}

.step-icon.done {
  background: var(--primary);
}

.step-icon.current {
  background: var(--primary);
}

.step-number {
  font-size: 24rpx;
  color: var(--white);
  font-weight: 700;
}

.step-line {
  flex: 1;
  height: 4rpx;
  background: var(--greyLight-2);
  border-radius: 2rpx;
  margin: 28rpx 8rpx 0;
}

.step-line.done {
  background: var(--primary);
}

.step .forum-caption {
  margin-top: 8rpx;
  font-size: 20rpx;
}

.step .forum-caption.primary {
  color: var(--primary);
}

/* Countdown */
.countdown-card {
  padding: 32rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.countdown-row {
  display: flex;
  align-items: center;
  margin-top: 16rpx;
}

.countdown-box {
  width: 96rpx;
  height: 96rpx;
  border-radius: var(--forum-radius-sm);
  margin: 0 16rpx;
}

.countdown-labels {
  display: flex;
  margin-top: 16rpx;
}

.countdown-labels .forum-caption {
  margin: 0 48rpx;
  font-size: 20rpx;
}

/* Avatar */
.avatar-card {
  padding: 32rpx;
}

.avatar-main {
  display: flex;
  align-items: center;
  margin-bottom: 24rpx;
}

.avatar-wrapper {
  position: relative;
  margin-right: 24rpx;
}

.avatar-wrapper.small {
  margin-right: 24rpx;
}

.avatar-large {
  width: 104rpx;
  height: 104rpx;
  /* border-radius: 50%; */
  border-radius: 12px;
  box-shadow: var(--neu-shadow-out);
}

.avatar-text-large {
  font-size: 40rpx;
  color: var(--white);
  font-weight: 700;
}

.avatar-small {
  width: 80rpx;
  height: 80rpx;
  /* border-radius: 50%; */
  border-radius: 12px;
}

.avatar-text-small {
  font-size: 28rpx;
  color: var(--white);
  font-weight: 700;
}

.online-dot {
  position: absolute;
  bottom: 4rpx;
  right: 4rpx;
  width: 28rpx;
  height: 28rpx;
  background: var(--state-success);
  border-radius: 50%;
  box-shadow: var(--neu-shadow-sm);
  border: 4rpx solid var(--greyLight-1);
}

.online-dot.small {
  width: 20rpx;
  height: 20rpx;
}

.offline-dot {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 20rpx;
  height: 20rpx;
  background: var(--greyLight-2);
  border-radius: 50%;
  border: 4rpx solid var(--greyLight-1);
}

.busy-dot {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 20rpx;
  height: 20rpx;
  background: var(--state-error);
  border-radius: 50%;
  border: 4rpx solid var(--greyLight-1);
}

.avatar-info {
  display: flex;
  flex-direction: column;
}

.avatar-info .forum-body.bold {
  font-weight: 600;
}

.avatar-row {
  display: flex;
  align-items: center;
  margin-top: 24rpx;
}

.avatar-add {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
}

/* Back to Top */
.back-to-top {
  display: flex;
  justify-content: flex-end;
  padding-right: 16rpx;
}

/* Custom Navbar */
.custom-navbar {
  padding: 0;
  overflow: hidden;
}

.navbar-top {
  display: flex;
  align-items: center;
  padding: 24rpx 32rpx;
  min-height: 96rpx;
}

.navbar-left,
.navbar-right {
  flex: 1;
  display: flex;
  align-items: center;
}

.navbar-right {
  justify-content: flex-end;
}

.navbar-divider {
  height: 2rpx;
  background: var(--greyLight-2);
}

.navbar-actions {
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding: 24rpx 32rpx;
  min-height: 96rpx;
}

.action-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.action-label {
  font-size: 20rpx;
  color: var(--forum-muted-foreground);
  margin-top: 4rpx;
}

.action-label.error {
  color: var(--state-error);
}

.action-label.warning {
  color: var(--state-warning);
}


.author-box{
    position: relative;
    transition: all 0.3s;
    overflow: hidden;
    border-radius: 12px;
    box-sizing: border-box;
    margin: 20px;
    padding: 20px 15px;
    height: auto;
    
    &::after {
        font-family: uvicon-iconfont;
        content: "\e640";
        font-size: 140px;
        color: var(--primary);
        position: absolute;
        right: 0;
        top: -50%;
        
    }
    
    &.card-style{
        overflow: hidden;
        height: 40px !important;
        padding: 0;
        margin: 0;
        
        &.card-style::after{
            /* 吸顶状态时, 隐藏图标 */
            content: "";
        }
    }
    
    .author-box__title{
        transition: all 0.3s;
        margin-bottom: 20px;
        
        .title{
            box-sizing: border-box;
            display: inline-block;
            border: var(--primary) solid 1px;
            color: var(--primary);
            font-size: 15px;
            font-weight: bold;
            border-radius: 50px;
            padding: 5px 35px;
            margin-left: 10px;
        }
    }
    
    .author{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center; 
        box-sizing: border-box;
        padding: 0 0 0 10px;
        height: 40px;
        background-color: var(--greyLight-1);
        
        z-index: 999;
        transition: all 0.3s;
        
        .left{
            display: flex; justify-content: flex-start; align-items: flex-start;
            transition: all 0.3s;
            width: 0px;
        }
        /*  动画效果-扩大宽度*/
        .left.show-width{
            width: 50px;
        }
        
        .author-info{
            display: flex;
            flex-direction: row;
            justify-content: center; 
            align-items: center; 
            transition: all 0.3s;
            
            .avatar-pic{
                margin: 0 10px;
                transition: all 0.3s;
            }
            .author-name{
                transition: all 0.3s;
                min-width: 0;
                max-width: 8em;
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
                font-size: 12px;
                color: var(--greyDark);
            }
        }
        
        .btn-list{
            display: flex;
            flex-direction: row;
            flex: 1;
             justify-content: space-around;
             align-items: center;
             transition: all 0.3s;
            
            .btn-item{
                justify-content: center;
                align-items: center; 
                text-align: center;
                transition: all 0.3s;
            }
        }
    }
}
</style>
