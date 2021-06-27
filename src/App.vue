<template>
  <div id="app">
    <button v-if="startStop" @click="start">start</button>
    <button v-else @click="stop">stop</button>
    <input v-model="interval" type="text" />
    <Bubble :info="info" :count="count" />
  </div>
</template>



<script>
import Bubble from "./components/Bubble";

export default {
  name: "App",
  components: {
    Bubble,
  },
  created() {
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
  },
  mounted() {
    this.modalShow = true;
  },
  destroyed() {
    window.removeEventListener("resize", this.handleResize);
  },
  updated() {
    if (this.info.length >= 5) {
      this.info.shift();
    }
  },
  methods: {
    start: function () {
      this.startStop = false;
      if (this.interval > 0) {
        this.intervalid1 = setInterval(() => {
          this.color = Math.floor(Math.random() * 16777215).toString(16);
          this.x = Math.floor(Math.random() * this.window.width) + 0;
          this.y = Math.floor(Math.random() * this.window.height) + 0;
          this.size = Math.floor(Math.random() * 85) + 15;
          this.info.push({
            background: "#" + this.color,
            width: this.size + "px",
            height: this.size + "px",
            x: this.x + "px",
            y: this.y + "px",
          });
        }, this.interval);
      }
    },
    stop: function () {
      this.startStop = true;
      clearInterval(this.intervalid1);
    },
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    },
  },
  data() {
    return {
      color: "",
      x: "",
      y: "",
      size: null,
      startStop: true,
      info: [],
      window: {
        width: 0,
        height: 0,
      },
      count: null,
      interval: null,
      modalShow: false,
    };
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  width: 100%;
  height: 100vh;
  position: relative;
}
</style>


