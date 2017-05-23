<template>
  <div class="main-window">
    <div class="view-area">{{ value }}</div>
    <div class="content-area">
      <number-button-group @number-change="numberChange"></number-button-group>
      <control-button-group @click-control="clickButton" @sum-result="sum">
      </control-button-group>
    </div>
  </div>
</template>

<script>
import NumberButtonGroup from './number-button-group'
import ControlButtonGroup from './control-button-group'

function calculate (temp, value, symbol) {
  switch (symbol) {
    case '+': return Number(temp) + Number(value)
    case '-': return Number(temp) - Number(value)
    case '*': return Number(temp) * Number(value)
    case '/': return Number(temp) / Number(value)
  }
}

export default {
  name: 'landing-page',

  data () {
    return {
      temp: '',
      value: '0',
      symbol: '',
      operation: false
    }
  },

  components: { NumberButtonGroup, ControlButtonGroup },

  methods: {
    numberChange (v) {
      if (this.symbol && !this.temp) {
        this.temp = this.value
        this.value = '0'
      }
      if (this.operation) this.value = '0'
      if (this.value.length >= 10) return
      if (this.value.length === 1) {
        this.operation = false
        if (this.value[0] === '0' && v !== '.') {
          if (v !== '00') this.value = v
        } else {
          this.value += v
        }
      } else {
        this.operation = false
        if (v === '.') {
          if (this.value.indexOf('.') === -1) this.value += v
        } else {
          this.value += v
        }
      }
    },

    clickButton (symbol) {
      const { temp, value } = this
      switch (symbol) {
        case '←':
          if (this.value.length > 1) {
            this.value = this.value.slice(0, -1)
          } else {
            this.value = '0'
          }
          break
        case 'AC':
          this.value = '0'
          this.temp = ''
          this.symbol = ''
          break
        default:
          if (symbol && value && temp) {
            this.value = calculate(temp, value, symbol)
            this.symbol = ''
            this.temp = ''
          } else {
            this.symbol = symbol
          }
      }
    },

    sum () {
      const { value, temp, symbol } = this
      if (symbol && value && temp) {
        this.value = calculate(temp, value, symbol)
        this.symbol = ''
        this.temp = ''
        this.operation = true
      }
    }
  }
}
</script>

<style lang="stylus">
.main-window
  height: 100%
  display: flex
  flex-direction: column

  .view-area
    flex: 1
    color: #fff
    display: flex
    padding: 10px
    font-size: 24px
    text-align: right
    align-items: flex-end
    background-color: #555
    flex-direction: column-reverse

  .content-area
    flex: 5
    display: flex
</style>
