<script>
export default {
  onLaunch: function () {},
  onShow: function () {},
  onHide: function () {}
}
</script>

<style lang="scss">
@import './uni_modules/zebra-ui/index';
// 这里定义了一些基础属性， 深色模式样式
@import './common/style/var';
@import './common/style/icon.css';

@import '@/styles/tool-rpx.css';
@import '@/styles/tool-px.css';
@import '@/styles/aye.scss';

/* 变量定义 */
:root {
    // --primary-light: #2fe25f;
    // --primary: #07c160;
    // --primary-dark: #0eb805;
    // --secondary-light: #8abdff;
    // --secondary: #6d5dfc;
    // --secondary-dark: #5b0eeb;
    // --white: #FFFFFF;
    // --greyLight-1: #E4EBF5;
    // --greyLight-2: #c8d0e7;
    // --greyLight-3: #bec8e4;
    // --greyDark: #9baacf;
    
    // --blackDark: #333;
    // --greyLight-1-dark: #d8e4f5;
    
    // --white: #ffffff;
    // --greyLight-1: #e2e2e2;
    // --greyLight-2: #c5c1c1;
    // --greyLight-3: #a7a1a1;
    // --greyDark: #8a98bb;
    
    /* 卡片外阴影样式 */
    --aye-shadow:  3px 3px 6px var(--greyLight-2), -2px -2px 5px var(--white);
}
 
::-webkit-scrollbar {
  width: 0;
  background: transparent;
}
</style>
