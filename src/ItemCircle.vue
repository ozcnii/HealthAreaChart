<template>
  <div class="item-test" :style="{ transform }" @click="$emit('click')">
    {{ index + 1 }}
  </div>
</template>

<script>
import { CENTER_ANGLE_DEG_OFFSET } from "./constants";

export default {
  emits: ["click"],

  props: {
    index: Number,
    count: Number,
    chartAngle: Number,
  },

  data() {
    return {
      wrapperHeight: 0,
    };
  },

  computed: {
    transform() {
      const positionRotate =
        (360 / this.count) * this.index + CENTER_ANGLE_DEG_OFFSET;

      const selfRotate =
        360 -
        ((360 / this.count) * this.index +
          this.chartAngle +
          CENTER_ANGLE_DEG_OFFSET);

      return `rotate(${positionRotate}deg) translate(calc(${this.wrapperHeight}px/2)) rotate(${selfRotate}deg)`;
    },
  },

  mounted() {
    this.wrapperHeight = this.$el?.parentNode.clientHeight;
  },
};
</script>

<style scoped>
.item-test {
  width: 45px; /* TODO: on small screen =45  */
  /* width: 45px; */
  height: 45px;
  background-color: red;
  position: absolute;

  background-color: #3498db;
  color: white;
  text-align: center;
  line-height: 40px;
  border-radius: 50%;
  position: absolute;
  inset: 162.5px; /* TODO: wrapper.height/2 - item.height/2 */

  cursor: pointer;

  transition: transform 0.4s cubic-bezier(0.67, 0.49, 0.21, 1.66);
}
</style>
