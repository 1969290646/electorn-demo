<template>
  <div class="number-button-area">
    <div class="row" v-for="buttons in buttonGroup" :key="buttons">
      <button
        v-for="button in buttons"
        :key="button" class="item"
        @click="$emit('number-change', button)">
        {{ button }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  created () {
    this.buttonGroup = [['7', '8', '9'], ['4', '5', '6'], ['1', '2', '3'], ['0', '00', '.']]
  }
}
</script>

<style lang="stylus">
.number-button-area
  flex: 3
  display: flex
  flex-wrap: wrap

  .row
    flex-basis: 100%
    display: flex

    .item
      flex: 1
      font-size: 32px
      cursor: pointer
</style>
