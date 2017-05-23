<template>
  <div class="control-button-area">
    <div class="row" v-for="buttons in buttonGroup" :key="buttons">
      <button
        v-for="button in buttons"
        :key="button" class="item"
        @click="$emit('click-control', button)">
        {{ button }}
      </button>
    </div>
    <div class="row">
      <button class="item" @click="$emit('sum-result')">=</button>
    </div>
  </div>
</template>

<script>
export default {
  created () {
    this.buttonGroup = [['←', 'AC'], ['+', '-'], ['*', '/']]
  }
}
</script>

<style lang="stylus">
.control-button-area
  flex: 2
  display: flex
  flex-wrap: wrap

  .row
    flex-basis: 100%
    display: flex

    button
      flex: 1
      font-size: 32px
      cursor: pointer
</style>
