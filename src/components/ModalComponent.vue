<template>
  <div>
    <div>
      <p>Select element to add:</p>
    </div>
    <div>
      <canvas width="140" height="80" id="condition" @click="action(1)"></canvas>
      <canvas width="140" height="80" id="action" @click="action(2)"></canvas>
    </div>
  </div>
</template>

<script>
export default {
  name: 'modal-component',
  methods: {
    action (value) {
      const a = this.arr.slice()
      a[this.addingValue] = value
      a[this.addingValue * 2] = 0
      a[this.addingValue * 2 + 1] = 0
      this.$emit('change', a, value)
    }
  },
  props: {
    addingValue: {
      type: Number,
      required: false,
      default: -1
    },
    arr: {
      type: Array,
      required: false,
      default: []
    }
  },
  mounted () {
    var c = document.getElementById('condition')
    var ctx = c.getContext('2d')
    ctx.beginPath()
    ctx.moveTo(10, 10)
    ctx.lineTo(120, 10)
    ctx.quadraticCurveTo(130, 10, 130, 20)
    ctx.lineTo(130, 50)
    ctx.quadraticCurveTo(130, 60, 120, 60)
    ctx.lineTo(10, 60)
    ctx.quadraticCurveTo(0, 60, 0, 50)
    ctx.lineTo(0, 20)
    ctx.quadraticCurveTo(0, 10, 10, 10)
    ctx.fillStyle = 'rgb(46, 138, 227)'
    ctx.strokeStyle = 'rgb(194, 224, 250)'
    ctx.lineWidth = 3
    ctx.fill()
    ctx.stroke()
    ctx.beginPath()
    ctx.moveTo(60, 25)
    ctx.lineTo(70, 25)
    ctx.lineTo(77, 35)
    ctx.lineTo(70, 45)
    ctx.lineTo(60, 45)
    ctx.lineTo(53, 35)
    ctx.closePath()
    ctx.lineWidth = 2
    ctx.strokeStyle = 'white'
    ctx.stroke()

    c = document.getElementById('action')
    ctx = c.getContext('2d')
    ctx.beginPath()
    ctx.moveTo(10, 10)
    ctx.lineTo(120, 10)
    ctx.quadraticCurveTo(130, 10, 130, 20)
    ctx.lineTo(130, 50)
    ctx.quadraticCurveTo(130, 60, 120, 60)
    ctx.lineTo(10, 60)
    ctx.quadraticCurveTo(0, 60, 0, 50)
    ctx.lineTo(0, 20)
    ctx.quadraticCurveTo(0, 10, 10, 10)
    ctx.closePath()
    ctx.fillStyle = 'rgb(207, 88, 228)'
    ctx.fill()
    ctx.beginPath()
    ctx.moveTo(65, 25)
    ctx.lineTo(53, 45)
    ctx.lineTo(78, 45)
    ctx.closePath()
    ctx.lineWidth = 2
    ctx.strokeStyle = 'white'
    ctx.stroke()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
