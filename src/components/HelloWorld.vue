<template>
  <div id="container" v-bind:style="{ width: width + 'px' }">
    <div class="download">
      <button @click="download">Save</button>
      <a id="downloadAnchorElem" style="display:none"></a>
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
      modal.style.left = window.scrollX + window.innerWidth / 2 - 150 + 'px'
      modal.style.top = window.scrollY + window.innerHeight / 10 * 3 + 'px'
      this.addingValue = value
      this.height = height
    },
    download () {
      var storageObj = {
        name: '',
        left: {},
        right: {}
      }
      for (var i = 1; i < this.arr.length; i++) {
        if (this.arr[i] !== 1 && this.arr[i] !== 2) {
          continue
        }
        var startObj = storageObj
        var index = i
        while (index > 1) {
          if (index % 2 === 0) {
            startObj = startObj['left']
            if (typeof (startObj['name']) === 'undefined') {
              startObj['name'] = ''
              startObj['left'] = {}
              startObj['right'] = {}
            }
          } else {
            startObj = startObj['right']
            if (typeof (startObj['name']) === 'undefined') {
              startObj['name'] = ''
              startObj['left'] = {}
              startObj['right'] = {}
            }
          }
          index = Math.floor(index / 2)
        }
        if (this.arr[i] === 1) {
          startObj['name'] = 'Condition'
        } else if (this.arr[i] === 2) {
          startObj['name'] = 'Action'
        }
      }
      var dataStr = 'data:text/json;charset=utf-8,' + encodeURIComponent(JSON.stringify(storageObj))
      var dlAnchorElem = document.getElementById('downloadAnchorElem')
      dlAnchorElem.setAttribute('href', dataStr)
      dlAnchorElem.setAttribute('download', 'data.json')
      dlAnchorElem.click()
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
  left: calc(50% - 150px);
  width: 300px;
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
