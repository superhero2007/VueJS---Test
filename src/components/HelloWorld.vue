<template>
  <div id="container" v-bind:style="{ width: width + 'px' }">
    <div class="download">
      <button @click="download">Save</button>
    </div>
    <node-component :value="1" :arr="arr" @adding="adding" :height="0">
    </node-component>
    <modal-component :addingValue="addingValue" :arr="arr" @change='change' v-show="addingValue != -1" id="modalBox">
    </modal-component>
  </div>
</template>

<script>
import NodeComponent from './NodeComponent'
import ModalComponent from './ModalComponent'
export default {
  name: 'HelloWorld',
  components: {
    NodeComponent,
    ModalComponent
  },
  methods: {
    change (a, value) {
      if (value === 2) {
        this.height = this.height - 1
      }
      this.arr = a
      var width = Math.pow(2, this.height) * 400
      if (width > this.width) {
        this.width = width
      }
      this.addingValue = -1
    },
    adding (value, height) {
      var modal = document.getElementById('modalBox')
      modal.style.left = window.scrollX + window.innerWidth / 2 - 200 + 'px'
      modal.style.top = window.scrollY + window.innerHeight / 10 * 3 + 'px'
      this.addingValue = value
      this.height = height
    },
    download () {
      var jsonObj = {
        name: '',
        leftChild: {},
        rightChild: {}
      }
      for (var i = 1; i < this.arr.length; i++) {
        if (this.arr[i] !== 1 && this.arr[i] !== 2) {
          continue
        }
        var startObj = jsonObj
        var index = i
        var temp = []
        while (index > 1) {
          temp.push(index % 2)
          index = Math.floor(index / 2)
        }
        while (temp.length) {
          index = temp.pop()
          if (index % 2 === 0) {
            startObj = startObj['leftChild']
          } else {
            startObj = startObj['rightChild']
          }
        }
        if (this.arr[i] === 1) {
          startObj['name'] = 'Condition'
        } else if (this.arr[i] === 2) {
          startObj['name'] = 'Action'
        }
        startObj['leftChild'] = {}
        startObj['rightChild'] = {}
      }
      console.log(jsonObj)
    }
  },
  data () {
    return {
      arr: [0, 0],
      addingValue: -1,
      width: 0,
      height: 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#container {
  min-width: 100%;
}
#modalBox {
  position: absolute;
  top: 30%;
  left: calc(50% - 200px);
  width: 400px;
  box-shadow: 0px 0px 15px 2px #ccc;
  padding: 10px;
  background: white;
}
.download {
  position: absolute;
  top: 20px;
  left: 20px;
}
</style>
