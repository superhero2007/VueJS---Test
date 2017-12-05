<template>
  <div class="element">
    <canvas width="150" height="75" class="action"></canvas>
    <slot/>
  </div>
</template>

<script>
export default {
  name: 'ActionComponent',
  methods: {
    draw () {
      var conditions = document.getElementsByClassName('action')
      for (var i = 0; i < conditions.length; i++) {
        var c = conditions[i]
        var parent = c.parentNode
        var width = parent.offsetWidth
        c.setAttribute('width', width)
        var ctx = c.getContext('2d')
        ctx.clearRect(0, 0, width, 75)

        ctx.moveTo(width / 2, 45)
        ctx.lineTo(width / 2, 73)
        ctx.lineWidth = 2
        ctx.strokeStyle = 'gray'
        ctx.stroke()

        ctx.beginPath()
        ctx.moveTo(width / 2 - 5, 65)
        ctx.lineTo(width / 2 + 5, 65)
        ctx.lineTo(width / 2, 75)
        ctx.closePath()
        ctx.fillStyle = 'gray'
        ctx.fill()

        ctx.beginPath()
        ctx.rect(width / 2 - 50, 5, 100, 40)
        ctx.arc(width / 2 + 50, 25, 20, 0, 2 * Math.PI)
        ctx.arc(width / 2 - 50, 25, 20, 0, 2 * Math.PI)
        ctx.closePath()
        ctx.fillStyle = 'rgb(207, 88, 228)'
        ctx.fill()
        ctx.fillStyle = 'white'
        ctx.font = '15px Verdana'
        ctx.fillText('Action', width / 2 - 75 + 50, 30)
      }
    }
  },
  mounted () {
    this.draw()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.element {
  position: relative;
}
.action {
  margin-bottom: -13px;
  margin-top: 5px;
}
canvas {
  margin: 0 auto;
  display: block;
}
.children {
  text-align: start;
}
</style>
