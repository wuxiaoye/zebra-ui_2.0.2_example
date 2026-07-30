<template>
  <DemoPage title="Cascader">
    <view class="demo-cascader">
      <!-- 基础用法 -->
      <demo-block title="基础用法">
        <z-field
          v-model="fieldValue"
          is-link
          readonly
          label="地区"
          placeholder="请选择所在地区"
          @click="showCascader()"
        />
        <z-popup
          v-model:show="show"
          round
          position="bottom"
          destroy-on-close
        >
          <z-cascader
            v-model="cascaderValue"
            title="请选择所在地区"
            :options="options"
            :lazy-render="true"
            @close="show = false"
            @finish="onFinish"
          />
        </z-popup>
      </demo-block>

      <!-- 完整省市区数据 -->
      <demo-block title="完整省市区数据">
        <z-field
          v-model="fieldValueAll"
          is-link
          readonly
          label="地区"
          placeholder="请选择所在地区"
          @click="showCascaderAll()"
        />
        <z-popup
          v-model:show="showAll"
          round
          position="bottom"
          destroy-on-close
        >
          <z-cascader
            v-model="cascaderValueAll"
            title="请选择所在地区"
            :options="optionsAll"
            :lazy-render="true"
            @close="showAll = false"
            @finish="onFinishAll"
          />
        </z-popup>
      </demo-block>

      <!-- 自定义颜色 -->
      <demo-block title="自定义颜色">
        <z-field
          v-model="fieldValueColor"
          is-link
          readonly
          label="地区"
          placeholder="请选择所在地区"
          @click="showCascaderColor()"
        />
        <z-popup
          v-model:show="showColor"
          round
          position="bottom"
          destroy-on-close
        >
          <z-cascader
            v-model="cascaderValueColor"
            title="请选择所在地区"
            :options="optionsColor"
            active-color="#ee0a24"
            :lazy-render="true"
            @close="showColor = false"
            @finish="onFinishColor"
          />
        </z-popup>
      </demo-block>

      <!-- 异步加载选项 -->
      <demo-block title="异步加载选项">
        <z-field
          v-model="fieldValueAsync"
          is-link
          readonly
          label="地区"
          placeholder="请选择所在地区"
          @click="showCascaderAsync()"
        />
        <z-popup
          v-model:show="showAsync"
          round
          position="bottom"
          destroy-on-close
        >
          <z-cascader
            v-model="cascaderValueAsync"
            title="请选择所在地区"
            :options="optionsAsync"
            :lazy-render="true"
            @close="showAsync = false"
            @change="onChangeAsync"
            @finish="onFinishAsync"
          />
        </z-popup>
      </demo-block>

      <!-- 自定义字段名 -->
      <demo-block title="自定义字段名">
        <z-field
          v-model="fieldValueCustom"
          is-link
          readonly
          label="地区"
          placeholder="请选择所在地区"
          @click="showCascaderCustom()"
        />
        <z-popup
          v-model:show="showCustom"
          round
          position="bottom"
          destroy-on-close
        >
          <z-cascader
            v-model="cascaderValueCustom"
            title="请选择所在地区"
            :options="optionsCustom"
            :field-names="fieldNames"
            :lazy-render="true"
            @close="showCustom = false"
            @finish="onFinishCustom"
          />
        </z-popup>
      </demo-block>

      <!-- 自定义选项上方内容 -->
      <demo-block title="自定义选项上方内容">
        <z-field
          v-model="fieldValueTop"
          is-link
          readonly
          label="地区"
          placeholder="请选择所在地区"
          @click="showCascaderTop()"
        />
        <z-popup
          v-model:show="showTop"
          round
          position="bottom"
          destroy-on-close
        >
          <z-cascader
            v-model="cascaderValueTop"
            title="请选择所在地区"
            :options="optionsTop"
            :lazy-render="true"
            @close="showTop = false"
            @finish="onFinishTop"
          >
            <template #options-top="{ tabIndex }">
              <div class="current-level">当前为第 {{ tabIndex + 1 }} 级</div>
            </template>
          </z-cascader>
        </z-popup>
      </demo-block>
    </view>
  </DemoPage>
</template>

<script lang="ts" setup>
import { ref, shallowRef } from 'vue'
import { useToast } from '../../uni_modules/zebra-ui'
import { useCascaderAreaData } from '../../common/js/area'

const toast = useToast()

// 弹窗显示状态
const show = ref(false)
const showColor = ref(false)
const showAsync = ref(false)
const showCustom = ref(false)
const showTop = ref(false)
const showAll = ref(false)

// 输入框展示文本
const fieldValue = ref('')
const fieldValueColor = ref('')
const fieldValueAsync = ref('')
const fieldValueCustom = ref('')
const fieldValueTop = ref('')
const fieldValueAll = ref('')

// 级联选中值初始化为空字符串，匹配 z-cascader 的 modelValue 类型 [Number, String]
const cascaderValue = ref('')
const cascaderValueColor = ref('')
const cascaderValueAsync = ref('')
const cascaderValueCustom = ref('')
const cascaderValueTop = ref('')
const cascaderValueAll = ref('')

// 树形Options使用shallowRef，禁止深度监听，根治递归更新
const options = shallowRef<any[]>([])
const optionsColor = shallowRef<any[]>([])
const optionsAsync = shallowRef<any[]>([])
const optionsCustom = shallowRef<any[]>([])
const optionsTop = shallowRef<any[]>([])
const optionsAll = shallowRef<any[]>([])

// 异步加载锁，防止重复请求触发多次渲染
const asyncLoadingLock = ref(false)

// 自定义字段映射
const fieldNames = {
  text: 'name',
  value: 'code',
  children: 'items'
}

// ========== 选中完成回调 ==========
const onFinish = ({ selectedOptions }: any) => {
  fieldValue.value = selectedOptions.map((opt: any) => opt.text).join('/')
  show.value = false
}

const onFinishColor = ({ selectedOptions }: any) => {
  fieldValueColor.value = selectedOptions.map((opt: any) => opt.text).join('/')
  showColor.value = false
}

const onFinishAsync = ({ selectedOptions }: any) => {
  fieldValueAsync.value = selectedOptions.map((opt: any) => opt.text).join('/')
  showAsync.value = false
}

const onFinishCustom = ({ selectedOptions }: any) => {
  fieldValueCustom.value = selectedOptions.map((opt: any) => opt.name).join('/')
  showCustom.value = false
}

const onFinishTop = ({ selectedOptions }: any) => {
  fieldValueTop.value = selectedOptions.map((opt: any) => opt.text).join('/')
  showTop.value = false
}

const onFinishAll = ({ selectedOptions }: any) => {
  fieldValueAll.value = selectedOptions.map((opt: any) => opt.text).join('/')
  showAll.value = false
}

// ========== 打开弹窗赋值Options ==========
const showCascader = () => {
  options.value = [
    {
      text: '浙江省',
      value: '330000',
      children: [{ text: '杭州市', value: '330100' }]
    },
    {
      text: '江苏省',
      value: '320000',
      children: [{ text: '南京市', value: '320100' }]
    }
  ]
  show.value = true
}

const showCascaderAll = () => {
  optionsAll.value = useCascaderAreaData()
  showAll.value = true
}

const showCascaderColor = () => {
  optionsColor.value = [
    {
      text: '浙江省',
      value: '330000',
      children: [{ text: '杭州市', value: '330100' }]
    },
    {
      text: '江苏省',
      value: '320000',
      children: [{ text: '南京市', value: '320100' }]
    }
  ]
  showColor.value = true
}

const showCascaderCustom = () => {
  optionsCustom.value = [
    {
      name: '浙江省',
      code: '330000',
      items: [{ name: '杭州市', code: '330100' }]
    },
    {
      name: '江苏省',
      code: '320000',
      items: [{ name: '南京市', code: '320100' }]
    }
  ]
  showCustom.value = true
}

const showCascaderAsync = () => {
  optionsAsync.value = [
    {
      text: '浙江省',
      value: '330000',
      children: []
    }
  ]
  asyncLoadingLock.value = false
  showAsync.value = true
}

const showCascaderTop = () => {
  optionsTop.value = [
    {
      text: '浙江省',
      value: '330000',
      children: [{ text: '杭州市', value: '330100' }]
    },
    {
      text: '江苏省',
      value: '320000',
      children: [{ text: '南京市', value: '320100' }]
    }
  ]
  showTop.value = true
}

// ========== 核心修复：异步加载change事件，杜绝原地修改触发递归 ==========
const onChangeAsync = ({ value }: any) => {
  if (asyncLoadingLock.value) return

  const targetItem = optionsAsync.value[0]
  if (value === targetItem.value && targetItem.children.length === 0) {
    asyncLoadingLock.value = true
    toast.showLoadingToast('加载中...')

    setTimeout(() => {
      // 整体重新赋值新数组，不修改原对象内部属性
      optionsAsync.value = [
        {
          ...targetItem,
          children: [
            { text: '杭州市', value: '330100' },
            { text: '宁波市', value: '330200' }
          ]
        }
      ]
      toast.closeToast()
      asyncLoadingLock.value = false
    }, 1000)
  }
}
</script>

<style lang="scss" scoped>
.demo-cascader {
  .current-level {
    padding: 32rpx 32rpx 0;
    font-size: 28rpx;
    color: var(--z-gray-6);
  }
}
</style>