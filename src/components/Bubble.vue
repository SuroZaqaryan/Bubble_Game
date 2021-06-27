<template>
  <div>
    <h3>count: {{ countBinding ? countBinding : "" }}</h3>
    <div v-for="(i, index) in infoColors" :key="index">
      <div
        class="bubble"
        @click="removeBubble(index)"
        :style="{
          width: i.width,
          height: i.height,
          background: i.background,
          left: i.x,
          top: i.y,
        }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    info: Array,
    count: Number,
  },

  methods: {
    removeBubble(index) {
      this.infoColors.splice(index, 1);
      this.countBinding++;
    },
  },
  data() {
    return {
      infoColors: this.info,
      countBinding: this.count,
    };
  },
};
</script>

<style>
.bubble {
  position: absolute;
  border-radius: 100%;
  cursor: pointer;
}
</style>


