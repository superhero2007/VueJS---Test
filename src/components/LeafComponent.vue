<template>
  <canvas width="20" height="20" class="leaf" @click="clicked"></canvas>
</template>
<script>
export default {
  methods: {
    clicked () {
      this.$emit('adding', this.value, this.height)
    },
    draw () {
      var leafs = document.getElementsByClassName('leaf')
      for (var i = 0; i < leafs.length; i++) {
        var leaf = leafs[i]
        var leafCtx = leaf.getContext('2d')
        leafCtx.fillStyle = 'rgb(46, 138, 227)'
        leafCtx.clearRect(0, 0, 20, 20)
        leafCtx.fillRect(0, 0, 20, 20)
        leafCtx.moveTo(3, 10)
        leafCtx.lineTo(17, 10)
        leafCtx.moveTo(10, 3)
        leafCtx.lineTo(10, 17)
        leafCtx.lineWidth = 2
        leafCtx.strokeStyle = 'white'
        leafCtx.stroke()
      }
    }
  },
  mounted () {
    this.draw()
  },
  props: {
    value: {
      type: Number,
      required: false,
      default: 0
    },
    height: {
      type: Number,
      required: false,
      default: 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
canvas {
  margin: 0 auto;
  display: block;
}
</style>
