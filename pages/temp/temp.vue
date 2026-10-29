<template>
    <view style="display: flex; flex: 1; flex-direction: column; justify-content: center; align-items: center; padding-bottom: 80px;">
        
        <view>
            <uv-button text="登录" type="success" @tap="click_tab"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="初始拟物 UI" type="success" @tap="click_ui"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="绿色拟物 UI" type="success" @tap="click_ui2"></uv-button>
        </view>
        
        <view style="margin-top: 2em;">
            <uv-button text="UI 组件库 - AI 设计" type="primary" @tap="click_index('ui-components')"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="UI-首页" type="primary" @tap="click_index('home-page')"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="UI-帖子详情页" type="primary" @tap="click_index('post-detail')"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="UI-榜单" type="primary" @tap="click_index('ranking')"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="UI-消息中心" type="primary" @tap="click_index('messages')"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="UI-论坛板块" type="primary" @tap="click_index('forum')"></uv-button>
        </view>
        <view style="margin-top: 2em;">
            <uv-button text="UI-聊天窗口" type="primary" @tap="click_index('chat')"></uv-button>
        </view>
        
    </view>
</template>

<script>
    
export default {
    setup() {
        return {
        }
    },
    data(){
        return {
            
        }
    },
    onShow() {
        //隐藏原生底部导航栏
        // uni.hideTabBar();
    },
    methods: {
        
        click_index(e){
            switch (e){
                case 'chat': uni.navigateTo({ url: '/pages/ui/chat' })
                    break;
                case 'forum': uni.navigateTo({ url: '/pages/ui/forum' })
                    break;
                case 'home-page': uni.navigateTo({ url: '/pages/ui/home-page' })
                    break;
                case 'messages': uni.navigateTo({ url: '/pages/ui/messages' })
                    break;
                case 'post-detail': uni.navigateTo({ url: '/pages/ui/post-detail' })
                    break;
                case 'ranking': uni.navigateTo({ url: '/pages/ui/ranking' })
                    break;
                case 'ui-components': uni.navigateTo({ url: '/pages/ui/ui-components' })
                    break;
                default:
                    break;
            }
        },
        click_ui2(){
            uni.navigateTo({
                url: '/pages/ui/ui2'
            })
        },
        click_ui(){
            console.log('初始拟物 UI')
            uni.navigateTo({
                url: '/pages/ui/ui'
            })
        },
        click_tab(){
            uni.navigateTo({
                url: '/pages/login/login'
            })
        }
    }
}
</script>

<style>
           
</style>
