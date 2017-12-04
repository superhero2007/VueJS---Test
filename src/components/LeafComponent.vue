<template>
  <canvas width="15" height="15" class="leaf" @click="clicked"></canvas>
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
        leafCtx.clearRect(0, 0, 15, 15)
        leafCtx.fillRect(0, 0, 15, 15)
        leafCtx.moveTo(3, 8)
        leafCtx.lineTo(13, 8)
        leafCtx.moveTo(8, 3)
        leafCtx.lineTo(8, 13)
        leafCtx.lineWidth = 1
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
