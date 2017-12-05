<template>
  <div>
    <div>
      <p>Select element to add:</p>
    </div>
    <div>
      <button class="conditionButton"><canvas width="170" height="70" id="conditioncanvas" @click="action(1)"></canvas></button>
      <button class="actionButton"><canvas width="170" height="70" id="actioncanvas" @click="action(2)"></canvas></button>
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
    let c = document.getElementById('conditioncanvas')
    let ctx = c.getContext('2d')
    ctx.beginPath()
    ctx.moveTo(10, 0)
    ctx.lineTo(160, 0)
    ctx.quadraticCurveTo(170, 0, 170, 10)
    ctx.lineTo(170, 60)
    ctx.quadraticCurveTo(170, 70, 160, 70)
    ctx.lineTo(10, 70)
    ctx.quadraticCurveTo(0, 70, 0, 60)
    ctx.lineTo(0, 10)
    ctx.quadraticCurveTo(0, 0, 10, 0)
    ctx.closePath()
    ctx.fillStyle = 'rgb(46, 138, 227)'
    ctx.strokeStyle = 'rgb(194, 224, 250)'
    ctx.lineWidth = 3
    ctx.fill()

    ctx.beginPath()
    ctx.moveTo(70, 15)
    ctx.lineTo(100, 15)
    ctx.lineTo(110, 35)
    ctx.lineTo(100, 55)
    ctx.lineTo(70, 55)
    ctx.lineTo(60, 35)
    ctx.closePath()
    ctx.lineWidth = 2
    ctx.strokeStyle = 'white'
    ctx.stroke()

    c = document.getElementById('actioncanvas')
    ctx = c.getContext('2d')
    ctx.beginPath()
    ctx.moveTo(10, 0)
    ctx.lineTo(160, 0)
    ctx.quadraticCurveTo(170, 0, 170, 10)
    ctx.lineTo(170, 60)
    ctx.quadraticCurveTo(170, 70, 160, 70)
    ctx.lineTo(10, 70)
    ctx.quadraticCurveTo(0, 70, 0, 60)
    ctx.lineTo(0, 10)
    ctx.quadraticCurveTo(0, 0, 10, 0)
    ctx.closePath()
    ctx.fillStyle = 'rgb(207, 88, 228)'
    ctx.fill()

    ctx.beginPath()
    ctx.moveTo(85, 20)
    ctx.lineTo(65, 50)
    ctx.lineTo(105, 50)
    ctx.closePath()
    ctx.lineWidth = 2
    ctx.strokeStyle = 'white'
    ctx.stroke()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
button {
  background: transparent;
  color: transparent;
  border-radius: 13px;
  outline: 0;
  padding: 0;
  height: 74px;
  border: 3px solid transparent;
}
.conditionButton:focus, .conditionButton:hover {
  border: 3px solid rgb(194, 224, 250); 
}
.actionButton:focus, .actionButton:hover {
  border: 3px solid rgb(240, 203, 247); 
}
</style>
