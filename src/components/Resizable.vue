<template>
  <div>
    <div class="container">
      <div class="top">Parent Window</div>
      <vue-resizable
        class="resizable"
        ref="resizableComponent"
        :active="handlers"
        :fit-parent="fit"
        :max-width="maxW | checkEmpty"
        :max-height="maxH | checkEmpty"
        :min-width="minW | checkEmpty"
        :min-height="minH | checkEmpty"
        :width="width"
        :height="height"
        :left="left"
        :top="top"
        @mount="eHandler"
        @resize:move="eHandler"
        @resize:start="eHandler"
        @resize:end="eHandler"
      >
        <div class="block">
          <div class="drag-container-1">Child Window</div>
          <div class="table-container">
            <!--  <ChildWindow /> -->
            <!--  <table>
              <tr>
                <td>w:{{width}}</td>
                <td>h:{{height}}</td>
              </tr>
              <tr>
                <td>l:{{left}}</td>
                <td>t:{{top}}</td>
              </tr>
            
            </table>-->
          </div>
          <!--  <div class="drag-container-2">drag_2</div> -->
        </div>
      </vue-resizable>
    </div>
   
  </div>
</template>

<script>
import VueResizable from "vue-resizable";
/* import ChildWindow from './ChildWindow.vue'; */
export default {
  name: "Resizable",
  components: { VueResizable /* ,ChildWindow  */ },
  data() {
    const tW = 800;
    const tH = 600;
    return {
      handlers: ["r", "rb", "b"],
      left: 20,
      top: 10,
      height: tH,
      width: tW,
      maxW: 1000,
      maxH: 500,
      minW: 100,
      minH: 100,
      fit: true,
      event: "",
      dragSelector: ".drag-container-1, .drag-container-2"
    };
  },
  methods: {
    eHandler(data) {
      this.width = data.width;
      this.height = data.height;
      this.left = data.left;
      this.top = data.top;
      this.event = data.eventName;
    }
  },
  filters: {
    checkEmpty(value) {
      return typeof value !== "number" ? 0 : value;
    }
  }
};
</script>

<style scoped>
.block {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
<style>
body,
html {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
  overflow: auto;
}

.container {
  width: 1000px;
  height: 600px;
  display: inline-block;
  background: #ffffff;
  color: #333333;
  margin: 10px;
  border: 3px solid #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}

#block1 {
  border: solid black 1px;
  height: 300px;
  width: 300px;
  display: inline-block;
  float: left;
}

.resizable {
  background-position: top left;
  width: 150px;
  height: 150px;
  padding: 0;
  border: 3px solid #f1f1f1;
  /* background: #007fff; */
  font-weight: normal;
  position: relative;
}

.table-block {
  display: table;
}

.table-row {
  display: table-row;
  text-align: center;
}

.table-cell {
  width: 50%;
  display: inline-block;
}

.table-input {
  width: 50px;
}

.drag-container-1,
.drag-container-2 {
  width: 100%;
  height: 20px;
  background: #f1f1f1;
  text-align: center;
  cursor: pointer;
}

.table-container {
  flex: 1;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.top {
  padding: 10px;
  background: #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}
</style>