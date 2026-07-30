<script>
export default {
  onLaunch: function () {},
  onShow: function () {},
  onHide: function () {}
}
</script>

<style lang="scss">
@import './uni_modules/zebra-ui/index';
@import './common/style/var';
@import './common/style/icon.css';

@import '@/styles/tool-rpx.css';
@import '@/styles/tool-px.css';
@import '@/styles/aye.scss';

/* 变量定义 */
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
}
 
::-webkit-scrollbar {
  width: 0;
  background: transparent;
}
</style>
