<template>
  <view class="search">
    <input class="search__input" :placeholder="placeholder" :value="modelValue" @input="onInput" placeholder-class="search-placeholder" />
    <view class="search__icon">
        <text class="ayeIconfont aye-icon-Search"></text>
    </view>
  </view>
</template>

<script setup>
const props = defineProps({
  modelValue: { type: String, default: '' },
  placeholder: { type: String, default: '请输入文字...' }
});
const emit = defineEmits(['update:modelValue']);
const onInput = (e) => emit('update:modelValue', e.detail.value);
</script>

<style scoped>
:root {
  --greyLight-1: #E4EBF5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #FFFFFF;
}
@font-face {
  font-family: "ayeIconfont"; /* Project id 5208570 */
  /* 搜索图标 */
  src: 
       url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAAMAAAsAAAAABtwAAAKxAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHFQGYACCcAqBNIFIATYCJAMICwYABCAFhQsHMBsoBsgekiRFSDw4EEFIAEARD19r6Pt7GwRwJBF0VHRs6jpVrfU8vpqNuD/9uWA+VqbMFcNMw+9L6/mXBhGfxEa7nWPGN0bVlSNDduvn/5jpEtcg+YHmkp00sNl0ljTKvCo6wrvnB+A3jF3gEj4jUGtZBv/DgrI6FP1ChBepBbK6gzQ7Xhw2gkK5S5ZhtFqo7Hsyi08qSB/SDeRj+PPxnyWqSSoKVt7Zc74Vnf36bK8pxstxip8m5quDT0uoQIF5SCau2kMnAkQdIUCtKdAorM6CX5/L0teIXf/zRCUrsx70Q9Y9sV3OrWYmkOP+bcjDqJ2kLtLSQ6bi9MFv4ubexi7W3WLH6++UnUu+HI1nZ2bB+vbWfvhiJ725hcwe+onGB/vWvZ3sPtOrv7WBnBZ9maakRFOuPy7TB35tia7s2BFoS68r0zX/sq7EtoSEtsROVqLMVeZcK5VzRevpUS1Fxa4ZY4HcmdQe38T/wPTgfHtCZyLKglC+5Sje/da/cfXDldMZs391XQa/Xo/iQ04/C9XnNQU/cbqnjLLMwT2kfC0JAkmyRwUSam0vJcvW6n2srO1mY6FO2y1bqgymoFBnApqRy9AK5B60EnkMas2pZs62fliAyDWYtAZB6HQCkkafQaHTEzQj/yEVqKiAViL7QK2bWLmtzmS8P+BABFhx9wB2SMxLnYggA1CsDK4BW4+b8FI9JDYA9zl6sdlgqokWghf4dHt8vTaLEBRTzjy4gD0N3G6GZc6cIAmDXQg5xWikdd9ikJgH5eIAIQArrNsAzEHCeFF/OoEYAIq131MD2PRwI3h7G5C2AeB8HJPBzAxM/aCFIm/fpjv8ik8vGwtBoDCKYzywgnHLgJsbg8n1y5yARDCwjwjIUhjtTrSvyLC+xPM9mawNS57CXlSovATCJTtCAAAA') format('woff2');
}

.ayeIconfont {
  font-family: "ayeIconfont" !important;
  /* font-size: 16px; */
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: var(--greyDark);
  font-size: 32rpx;
}

.aye-icon-Search:before {
  content: "\e6cb";
}


.search {
  position: relative;
  display: flex;
  align-items: center;
}
.search__input {
  width: 100%;
  height: 80rpx;
  border: none;
  border-radius: 20rpx;
  font-size: 28rpx;
  padding-left: 76rpx;
  box-shadow: inset 4rpx 4rpx 10rpx var(--greyLight-2), inset -4rpx -4rpx 10rpx var(--white);
  background: none;
  color: var(--greyDark);
}
::v-deep .search-placeholder {
  color: var(--greyLight-3);
}
.search__icon {
  height: 40rpx;
  position: absolute;
  padding: 0 20rpx;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>