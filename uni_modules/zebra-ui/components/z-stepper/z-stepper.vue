<template>
  <view :class="bem([props.theme])">
    <view
      v-show="props.showMinus"
      :style="buttonStyle"
      :class="[
        bem('minus', { disabled: minusDisabled }),
        { [HAPTICS_FEEDBACK]: !minusDisabled }
      ]"
      @click="onClick($event, 'minus')"
      @touchstart.passive="onTouchstartPassive($event, 'minus')"
      @touchend="onTouchEnd"
      @touchcancel="onTouchEnd"
    >
        <text class="ayeIconfont aye-minus text-icon"></text>
    </view>
    <input
      v-show="props.showInput"
      :type="props.integer ? 'number' : 'digit'"
      :class="bem('input')"
      :value="current"
      :style="inputStyle"
      :disabled="props.disabled || props.disableInput"
      :inputmode="props.integer ? 'numeric' : 'decimal'"
      :placeholder="props.placeholder"
      :aria-valuemax="props.max"
      :aria-valuemin="props.min"
      :aria-valuenow="current"
      @blur="onBlur"
      @input="onInput"
      @focus="onFocus"
    />
    <view
      v-show="props.showPlus"
      :style="buttonStyle"
      :class="[
        bem('plus', { disabled: plusDisabled }),
        { [HAPTICS_FEEDBACK]: !plusDisabled }
      ]"
      @click="onClick($event, 'plus')"
      @touchstart.passive="onTouchstartPassive($event, 'plus')"
      @touchend="onTouchEnd"
      @touchcancel="onTouchEnd"
    >
        <text class="ayeIconfont aye-plus text-icon"></text>
    </view>
    
  </view>
</template>
<script lang="ts" setup>
import { ref, watch, computed, nextTick, type PropType } from 'vue'
import {
  isDef,
  addUnit,
  addNumber,
  truthProp,
  Interceptor,
  numericProp,
  formatNumber,
  getSizeStyle,
  createNamespace,
  callInterceptor,
  makeNumericProp,
  HAPTICS_FEEDBACK,
  LONG_PRESS_START_TIME,
  type Numeric,
  useCustomFieldValue,
  useComponentName
} from '../../libs/utils'

const [componentName, bem] = createNamespace('stepper')
useComponentName(componentName)

const LONG_PRESS_INTERVAL = 200

const isEqual = (value1?: Numeric, value2?: Numeric) =>
  String(value1) === String(value2)

const props = defineProps({
  min: makeNumericProp(1),
  max: makeNumericProp(Infinity),
  name: makeNumericProp(''),
  step: makeNumericProp(1),
  theme: String as PropType<any>,
  integer: Boolean,
  disabled: Boolean,
  showPlus: truthProp,
  showMinus: truthProp,
  showInput: truthProp,
  longPress: truthProp,
  autoFixed: truthProp,
  allowEmpty: Boolean,
  modelValue: numericProp,
  inputWidth: numericProp,
  buttonSize: numericProp,
  placeholder: String,
  disablePlus: Boolean,
  disableMinus: Boolean,
  disableInput: Boolean,
  beforeChange: Function as PropType<Interceptor>,
  defaultValue: makeNumericProp(1),
  decimalLength: numericProp
})

const emit = defineEmits([
  'plus',
  'blur',
  'minus',
  'focus',
  'change',
  'overlimit',
  'update:modelValue'
])

const format = (value: Numeric, autoFixed = true) => {
  const { min, max, allowEmpty, decimalLength } = props

  if (allowEmpty && value === '') {
    return value
  }

  value = formatNumber(String(value), !props.integer)
  value = value === '' ? 0 : +value
  value = Number.isNaN(value) ? +min : value

  value = autoFixed ? Math.max(Math.min(+max, value), +min) : value

  if (isDef(decimalLength)) {
    value = value.toFixed(+decimalLength)
  }

  return value
}

const getInitialValue = () => {
  const defaultValue = props.modelValue ? props.modelValue : props.defaultValue
  const value = format(defaultValue)

  if (!isEqual(value, props.modelValue)) {
    emit('update:modelValue', value)
  }

  return value
}

let actionType: 'plus' | 'minus'
const inputRef = ref<HTMLInputElement>()
const current = ref(getInitialValue())

const minusDisabled = computed(
  () => props.disabled || props.disableMinus || +current.value <= +props.min
)

const plusDisabled = computed(
  () => props.disabled || props.disablePlus || +current.value >= +props.max
)

const inputStyle = computed(() => ({
  width: addUnit(props.inputWidth),
  height: addUnit(props.buttonSize)
}))

const buttonStyle = computed(() => getSizeStyle(props.buttonSize))

const check = () => {
  const value = format(current.value)
  if (!isEqual(value, current.value)) {
    current.value = value
  }
}

const setValue = (value: Numeric) => {
  if (props.beforeChange) {
    callInterceptor(props.beforeChange, {
      args: [value],
      done() {
        current.value = value
      }
    })
  } else {
    current.value = value
  }
}

const onChange = () => {
  if (
    (actionType === 'plus' && plusDisabled.value) ||
    (actionType === 'minus' && minusDisabled.value)
  ) {
    emit('overlimit', actionType)
    return
  }

  const diff = actionType === 'minus' ? -props.step : +props.step
  const value = format(addNumber(+current.value, diff))

  setValue(value)
  emit(actionType)
}

const onInput = (event: any) => {
  const input = event.target as HTMLInputElement
  const { value } = input
  const { decimalLength } = props

  let formatted = formatNumber(String(value), !props.integer)

  if (isDef(decimalLength) && formatted.includes('.')) {
    const pair = formatted.split('.')
    formatted = `${pair[0]}.${pair[1].slice(0, +decimalLength)}`
  }

  if (props.beforeChange) {
    input.value = String(current.value)
  } else if (!isEqual(value, formatted)) {
    input.value = formatted
  }

  const isNumeric = formatted === String(+formatted)
  setValue(isNumeric ? +formatted : formatted)
}

const onFocus = (event: any) => {
  if (props.disableInput) {
    inputRef.value?.blur()
  } else {
    emit('focus', event)
  }
}

const onBlur = (event: any) => {
  const input = event.detail
  const value = format(input.value, props.autoFixed)
  input.value = String(value)
  current.value = value
  nextTick(() => {
    emit('blur', event)
  })
}

let longPressTimer: ReturnType<typeof setTimeout>

const longPressStep = () => {
  longPressTimer = setTimeout(() => {
    onChange()
    longPressStep()
  }, LONG_PRESS_INTERVAL)
}

const onTouchStart = () => {
  if (props.longPress) {
    clearTimeout(longPressTimer)
    longPressTimer = setTimeout(() => {
      onChange()
      longPressStep()
    }, LONG_PRESS_START_TIME)
  }
}

const onTouchEnd = (event: TouchEvent) => {
  if (props.longPress) {
    clearTimeout(longPressTimer)
  }
}

const onClick = (event: any, type: any) => {
  actionType = type
  onChange()
}
const onTouchstartPassive = (event: any, type: any) => {
  actionType = type
  onTouchStart()
}

watch(() => [props.max, props.min, props.integer, props.decimalLength], check)

watch(
  () => props.modelValue,
  (value) => {
    if (!isEqual(value, current.value)) {
      current.value = format(value!)
    }
  }
)

watch(current, (value) => {
  emit('update:modelValue', value)
  emit('change', value, { name: props.name })
})

useCustomFieldValue(() => props.modelValue)
</script>
<script lang="ts">
export default {
  name: 'ZStepper',
  options: {
    virtualHost: true
  }
}
</script>
<style lang="scss" scoped>
@font-face {
  font-family: "ayeIconfont"; /* Project id 5218209 */
  src: 
       url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAALkAAsAAAAABtAAAAKYAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHFQGYACDBgqBBIEVATYCJAMMCwgABCAFhQsHNhsVBsg+QTxgc6iipGmoUbtyXLPNKR55P5cB/CxGEg//7fe/fWbm3v/+3K/eBNGmzTKJ9RLqHU/iVawkMh1ChOqNUP7+r2mBVF91VYQ6ki2PyR7mH3B+RqDZqfkZy8IOmWMTNJT2fJTB7YjFCUm9IAdovhGCFus55eZBQJBIgfff6Ymgi96S5uf+GgBhoWIN/M//5fQmRoHMb1k5dUeNpWtsCuys9XzSaXPbWIRFEgA3jF3QEi8RqHaZqB1a2TqqdK/anFX6GkxqkMTH1dC3Kx1uURTo7wlt15VFvDLS4/QNL4PPxz9bj6TJzH2O/rJX+bC3jQfydx5FgOclNMjYpqIQx5s9fXVRxayrkgYMbxUhTWqfgNBk7Zb/eIlombFDYBMUp4siHT7B70+VQAYtGqx5DB9MIVcoQ2E9/1bvcXMYb1zpnur9Wp9E8+Cs0afcryNPIh7s6VK1+/Ff1RP2OXpfsoydTzEBtU4yfya/jreQ+7XfQpA+92/ywBTwE/8DVdFNR28PmuC10bwGFJ5JLiihkw2K/ENcCdWys8E0TPgbLpvsHEvoTCYgGbACss4qXPBdcIPvh1v8CKi22hdNNv5GXZRBrHmDIMx4B8mIryCb8QkX/B9qGDVwiy+C6lh279ZZ6+HB0Gb0wLmE0M0zYfvYvsR1ufMB+qeJTYViyDpBkmE96IpW4V/FDGm8OfLMN5gFCMpTWGHnYZLkUFAeoctKwFwMVFVUvUVx87SyiCAbQx7guARCrlxGePSY7RJaV7/nAPKdStiouQooeAIRKRwM0Cm0bvCqJOtadoPXSGd8BsYEIJBcCqwMG4YSiRwoqodFkIspggGuwoBq1RJdJcrysvR1t0Flzs6RIkfRXAuzU9m4mbjqSgU=') format('woff2');
}

.ayeIconfont {
  font-family: "ayeIconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  transition: all 0.3s ease;
}

.aye-minus:before {
  content: "\e6ba";
}

.aye-plus:before {
  content: "\e8fe";
}


.z-stepper {
  display: flex;
  align-items: center;
  user-select: none;

  &__minus,
  &__plus {
      cursor: pointer;
    position: relative;
    box-sizing: border-box;
    width: var(--z-stepper-input-height);
    height: var(--z-stepper-input-height);
    padding: 0;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    vertical-align: middle;
    border: 0;
    box-shadow: var(--z-stepper-btn-box-shadow);
    transition: all 0.3s ease;
  }

  &__minus {
    // border-radius: var(--z-stepper-radius) 0 0 var(--z-stepper-radius);
    border-radius: var(--z-stepper-radius);
    background-color: var(--z-stepper-btn-minus-background);
        .text-icon{
            color: var(--z-stepper-btn-minus-color);
        }
  }

  &__plus {
    // border-radius: 0 var(--z-stepper-radius) var(--z-stepper-radius) 0;
    border-radius: var(--z-stepper-radius);
    background-color: var(--z-stepper-btn-plus-background);
        .text-icon{
            color: var(--z-stepper-btn-plus-color);
        }
  }
  // disabled样式
    &__minus--disabled,
    &__plus--disabled {
      cursor: not-allowed;
      pointer-events: none;
        opacity: 0.6;
        
      box-shadow: 0 0 0;
      border: var(--greyLight-2) solid 1px;
      background-color: var(--greyLight-1);
       .text-icon{
           color: var(--greyLight-2);
       }
       
    }

  &__input {
    box-sizing: border-box;
    width: var(--z-stepper-input-width);
    height: var(--z-stepper-input-height);
    padding: 0;
    margin: 0 20rpx;
    font-size: var(--z-stepper-input-font-size);
    line-height: var(--z-stepper-input-line-height);
    color: var(--z-stepper-input-text-color);
    text-align: center;
    vertical-align: middle;
    appearance: none;
    background: var(--z-stepper-background);
    border: 0;
    border-width: 2rpx 0;
    border-radius: var(--z-stepper-input-border-radius);
    box-shadow: var(--z-stepper-input-box-shadow);

    &:disabled {
      color: var(--z-stepper-input-disabled-text-color);
      background-color: var(--z-stepper-input-disabled-background);
      -webkit-text-fill-color: var(--z-stepper-input-disabled-text-color);
      opacity: 1;
    }

    &:read-only {
      cursor: default;
    }
  }

  &--round {
    .z-stepper__plus,
    .z-stepper__minus {
      border-radius: 100%;
    }
  }
  
}
</style>
