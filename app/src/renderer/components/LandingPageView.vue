<template>
  <div class="main-window">
    <div class="view-area">{{ value }}</div>
    <div class="content-area">
      <number-button-group @number-change="numberChange"></number-button-group>
      <control-button-group @click-control="changeValue" @sum="sum"></control-button-group>
    </div>
  </div>
</template>

<script>
import NumberButtonGroup from './number-button-group'
import ControlButtonGroup from './control-button-group'

export default {
  name: 'landing-page',

  data () {
    return {
      temp: '',
      value: '0',
      symbol: ''
    }
  },

  components: { NumberButtonGroup, ControlButtonGroup },

  methods: {
    numberChange (v) {
      if (this.value.length >= 10) return
      if (this.symbol) {
        this.temp = this.value
        this.value = '0'
      }
      if (this.value.length === 1) {
        if (this.value[0] === '0' && v !== '.') {
          if (v !== '00') this.value = v
        } else {
          this.value += v
        }
      } else {
        if (v === '.') {
          if (this.value.indexOf('.') === -1) this.value += v
        } else {
          this.value += v
        }
      }
    },

    changeValue (v) {
      switch (v) {
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
          if (this.symbol) this.value = this.calculate()
          this.symbol = v
      }
    },

    calculate () {
      const { temp, value, symbol } = this
      this.symbol = ''
      switch (symbol) {
        case '+': return Number(value) + Number(temp)
        case '-': return Number(value) - Number(temp)
        case '*': return Number(value) * Number(temp)
        case '/': return Number(value) / Number(temp)
      }
    },

    sum () { if (this.symbol) this.calculate() }
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
    font-size: 36px
    text-align: right
    align-items: flex-end
    background-color: #555
    flex-direction: column-reverse

  .content-area
    flex: 5
    display: flex
</style>
