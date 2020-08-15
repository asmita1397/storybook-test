<template>
    
  <div class="container" ref="draggableContainer" id="draggable-container">
      <div class="top" id="draggable-header" @mousedown="dragMouseDown">
        <span class="dot"></span>
        <span class="dot"></span>
        <span class="dot"></span>
      </div>

      <div class="content" >
        <h3>Browser Window</h3>
        <p>How to create a browser window look with CSS.</p>
      </div>
    </div>
</template>


<script>
/* import  ParentWindow from "./ParentWindow" */
export default {
  name: 'DraggableDiv',
 /*  components:{
     ParentWindow
  }, */
  data: function () {
    return {
      positions: {
        clientX: undefined,
        clientY: undefined,
        movementX: 0,
        movementY: 0
      }
    }
  },
  methods: {
    dragMouseDown: function (event) {
      event.preventDefault()
      // get the mouse cursor position at startup:
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      document.onmousemove = this.elementDrag
      document.onmouseup = this.closeDragElement
    },
    elementDrag: function (event) {
      event.preventDefault()
      this.positions.movementX = this.positions.clientX - event.clientX
      this.positions.movementY = this.positions.clientY - event.clientY
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      // set the element's new position:
      this.$refs.draggableContainer.style.top = (this.$refs.draggableContainer.offsetTop - this.positions.movementY) + 'px'
      this.$refs.draggableContainer.style.left = (this.$refs.draggableContainer.offsetLeft - this.positions.movementX) + 'px'
    },
    closeDragElement () {
      document.onmouseup = null
      document.onmousemove = null
    }
  }
}
</script>



<style scoped>
#draggable-container {
  position: absolute;
  z-index: 9;
 /*  background-color: #f1f1f1; */
  text-align: center;
  border: 1px solid #d3d3d3;
  width:80%;
  
}

#draggable-header {
  padding: 10px;
  cursor: move;
  z-index: 10;
  
}
body {
  font-family: Arial;
}

* {
  box-sizing: border-box;
}

/* .dot {
  height: 12px;
  width: 12px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  float:right;
} */

.container {
  border: 3px solid #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;

}

.top {
  padding: 10px;
  background: #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  height:20%;
}

.content {
  padding: 10px;
  height:50%;
}

</style>