<template>
  <div>
    <condition-component v-if="arr[value] === 1">
      <div class="children">
        <div class="leftChild">
          <node-component :value='value * 2' :arr="arr" @adding='adding' :height="height + 1">
          </node-component>
        </div>
        <div class="rightChild">
          <node-component :value='value * 2 + 1' :arr="arr" @adding='adding' :height="height + 1">
          </node-component>
        </div>
      </div>
    </condition-component>
    <action-component v-if="arr[value] === 2">
      <div class="children">
        <div class="centerChild">
          <node-component :value='value * 2' :arr="arr" @adding='adding' :height="height">
          </node-component>
        </div>
      </div>
    </action-component>
    <leaf-component v-if="arr[value] != 1 && arr[value] != 2" :value='value' :height="height" @adding='adding'>
    </leaf-component>
   </div>
</template>

<script>
import ConditionComponent from './ConditionComponent'
import ActionComponent from './ActionComponent'
import LeafComponent from './LeafComponent'
export default {
  name: 'node-component',
  components: {
    ConditionComponent,
    ActionComponent,
    LeafComponent
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
    },
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
  methods: {
    adding (value, height) {
      this.$emit('adding', value, height)
    }
  },
  mounted () {
    var conditions = document.getElementsByClassName('condition')
    for (var i = 0; i < conditions.length; i++) {
      var c = conditions[i]
      var parent = c.parentNode
      var width = parent.offsetWidth
      c.setAttribute('width', width)
      var ctx = c.getContext('2d')
      ctx.fillStyle = 'rgb(46, 138, 227)'
      ctx.clearRect(0, 0, width, 75)

      var offset = width / 2 - 60
      ctx.moveTo(width / 2 - 75 + 145, 25)
      ctx.arcTo(width / 4 + offset + 50, 25, width / 4 + offset + 50, 50, 10)
      ctx.lineTo(width / 4 + offset + 50, 73)

      ctx.moveTo(width / 2 - 75 + 5, 25)
      ctx.arcTo(width / 4 + 5, 25, width / 4 + 5, 50, 10)
      ctx.lineTo(width / 4 + 5, 73)

      ctx.lineWidth = 3
      ctx.strokeStyle = 'gray'
      ctx.stroke()

      ctx.beginPath()
      ctx.moveTo(width / 4 + offset + 45, 65)
      ctx.lineTo(width / 4 + offset + 55, 65)
      ctx.lineTo(width / 4 + offset + 50, 75)
      ctx.closePath()
      ctx.fillStyle = 'gray'
      ctx.fill()

      ctx.beginPath()
      ctx.moveTo(width / 4 + 0, 65)
      ctx.lineTo(width / 4 + 10, 65)
      ctx.lineTo(width / 4 + 5, 75)
      ctx.closePath()
      ctx.fillStyle = 'gray'
      ctx.fill()

      ctx.beginPath()
      ctx.moveTo(width / 2 - 75 + 15, 5)
      ctx.lineTo(width / 2 - 75 + 135, 5)
      ctx.lineTo(width / 2 - 75 + 145, 25)
      ctx.lineTo(width / 2 - 75 + 135, 45)
      ctx.lineTo(width / 2 - 75 + 15, 45)
      ctx.lineTo(width / 2 - 75 + 5, 25)
      ctx.closePath()
      ctx.fillStyle = 'rgb(46, 138, 227)'
      ctx.fill()
      ctx.fillStyle = 'white'
      ctx.font = '15px Verdana'
      ctx.fillText('Condition', width / 2 - 75 + 40, 30)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
