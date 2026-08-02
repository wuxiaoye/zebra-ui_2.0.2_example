<template>
  <view class="demo-page">
        <aye-swiper-cube
          v-model="activeIndex2"
          :list="tabbarIcon"
          width="100vw"
          height="100vh"
          @change="onChange2"
        >
          <template #slide="{item, index}">
            <scroll-view
                style="height: 100vh;"
              scroll-y
            >
                  <cascaderPage v-if="index === 0" />
                  <fieldPage v-else-if="index === 1" />
                  <dialogPage v-else-if="index === 2" />
                  <cellPage v-else-if="index === 3" />
                  <buttonPage v-else-if="index === 4" />
            </scroll-view>
          </template>
        </aye-swiper-cube>
        
        <z-tabbar
          v-model="active"
          float
          background
          animate
          @change="tabbarChange"
        >
          <z-tabbar-item v-for="(item, index) in tabbarIcon" :key="index">
            <template #icon="props">
              <z-icon
                class-prefix="zebra-icon"
                :custom-style="{ 'font-weight': 'bold' }"
                :name="props.active ? item.active : item.inactive"
              />
            </template>
            {{ item.name }}
          </z-tabbar-item>
        </z-tabbar>
  </view>
</template>

<script>
import buttonPage from '@/pages/button/button.vue'
import cellPage from '@/pages/cell/cell.vue'
import dialogPage from '@/pages/dialog/dialog.vue'
import fieldPage from '@/pages/field/field.vue'
import cascaderPage from '@/pages/cascader/cascader.vue'

export default {
  components: { buttonPage, cellPage, dialogPage, fieldPage, cascaderPage },
  data() {
    return {
        activeIndex2: 0,
        active: 0,
        tabbarIcon : [
            {
            name: '第一',
            active: 'base-a',
            inactive: 'base'
            },
            {
            name: '第二',
            active: 'form-a',
            inactive: 'form-i'
            },
            {
            name: '第三',
            active: 'feedback-a',
            inactive: 'feedback'
            },
            {
            name: '第四',
            active: 'show-a',
            inactive: 'show'
            },
            {
            name: '第五',
            active: 'navigation-a',
            inactive: 'navigation'
            }
        ],
    }
  },
  onLoad() {
  },
  methods: {
    onChange2(index) {
      console.log('demo2 change:', index)
    },
    tabbarChange(e){
        console.log('切换导航栏', e)
        this.activeIndex2 = e;
    }
  }
}
</script>

<style scoped>
.demo-page {
  box-sizing: border-box;
}

</style>
