<template>
  <button class="cell" :class="[cell,{active,dead,flag,open,triggerDead}]"
          @mousedown.left="active=true"
          @mouseout.left="active=false"
          @mouseup="active=false"></button>
</template>

<script>
  export default {
    name: 'cell',
    props: ['data', 'rn', 'cn'],
    data () {
      return {open: false, flag: false, dead: false, triggerDead: false, active: false}
    },
    computed: {
      cell () {
        if (!this.open) return
        return this.data.mine ? 'mine' : 'n' + this.data.adjMine
      }
    },
    methods: {
      doOpen () {
        if (this.open || this.flag) return false
        this.open = true
        return true
      },
      mark () {
        if (this.open) return
        this.flag = !this.flag
        this.$emit('mark')
      }
    }
  }
</script>

<style scoped>
  .cell {
    display: inline-block;
    border: none;
    outline: none;
    width: 16px;
    height: 16px;
    background: url('sprite.png') no-repeat 0 -39px;
    margin: 0;
    padding: 0;
  }
  .cell:not(.open) {background-position: 0 -39px;}
  .cell.active {background-position: 0 -23px;}
  .cell.mine {background-position: -64px -39px;}
  .cell.flag {background-position: -16px -39px;}
  .cell.triggerDead {background-position: -32px -39px;}
  .cell.dead.flag:not(.mine) {background-position: -48px -39px;}
  .cell.n0 {background-position: 0 -23px;}
  .cell.n1 {background-position: -16px -23px;}
  .cell.n2 {background-position: -32px -23px;}
  .cell.n3 {background-position: -48px -23px;}
  .cell.n4 {background-position: -64px -23px;}
  .cell.n5 {background-position: -80px -23px;}
  .cell.n6 {background-position: -96px -23px;}
  .cell.n7 {background-position: -112px -23px;}
  .cell.n8 {background-position: -128px -23px;}
</style>
