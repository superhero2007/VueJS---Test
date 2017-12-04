<template>
  <div class="element">
    <canvas width="150" height="75" class="condition"></canvas>
    <slot/>
  </div>
</template>

<script>
export default {
  name: 'ConditionComponent'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.element {
  position: relative;
}
.condition {
  margin-bottom: -13px;
  margin-top: 13px;
}
canvas {
  margin: 0 auto;
  display: block;
}
.children {
  text-align: start;
}
.leftChild {
  position: absolute;
  width: 50%;
  left: 4px;
}
.rightChild {
  position: absolute;
  width: 50%;
  right: 11px;
}
</style>
