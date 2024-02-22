<template>
  <div class="wrapper" :style="{ transform: transformStyles }">
    <div class="chart-svg-container">
      <svg class="chart-svg">
        <chart-triangle
          v-for="(item, index) in items"
          :key="item.id"
          :index="index"
          :itemValue="item.value"
          :numTriangles="items.length"
          :activeTriangleIndex="activeTriangleIndex"
          @click="activateTriangleHandler(index)"
        />
      </svg>
    </div>

    <chart-area-circles :circles-values="CIRCLES_VALUES" />

    <item-circle
      @click="activateTriangleHandler(index)"
      v-for="(_, index) in items"
      :key="index"
      :index="index"
      :count="items.length"
      :chartAngle="chartAngle"
    />
  </div>
</template>

<script>
import ChartAreaCircles from "./ChartAreaCircles.vue";
import ChartTriangle from "./ChartTriangle.vue";
import ItemCircle from "./ItemCircle.vue";

import {
  CIRCLES_VALUES,
  CENTER_ANGLE_INDEX_OFFSET,
  CENTER_ANGLE_DEG_OFFSET,
} from "./constants";

export default {
  components: { ChartTriangle, ChartAreaCircles, ItemCircle },

  data() {
    return {
      activeTriangleIndex: -1,

      items: [
        { id: 1, value: 100 },
        { id: 2, value: 100 },
        { id: 3, value: 80 },
        { id: 4, value: 60 },
        { id: 5, value: 100 },
        { id: 6, value: 80 },
        { id: 7, value: 40 },
        { id: 8, value: 60 },
        { id: 9, value: 40 },
        { id: 10, value: 80 },
        { id: 11, value: 60 },
        { id: 12, value: 80 },
      ],
    };
  },

  computed: {
    transformStyles() {
      return `rotate(${this.chartAngle}deg)`;
    },

    chartAngle() {
      return (
        -(this.activeTriangleIndex - CENTER_ANGLE_INDEX_OFFSET) *
          (360 / this.items.length) +
        CENTER_ANGLE_DEG_OFFSET
      );
    },

    CIRCLES_VALUES() {
      return CIRCLES_VALUES;
    },

    CENTER_ANGLE_DEG_OFFSET() {
      return CENTER_ANGLE_DEG_OFFSET;
    },
  },

  methods: {
    activateTriangleHandler(index) {
      this.activeTriangleIndex = index;
    },
  },
};
</script>

<style scoped>
.wrapper {
  position: relative;
  width: min-content;
  transition: transform 0.4s cubic-bezier(0.67, 0.49, 0.21, 1.66);
}

.chart-svg-container {
  position: relative;
  width: 370px; /* = small -> 270 */
  height: 370px; /* = small -> 270 */
  border-radius: 100%;
  border: 2px solid #e8e9ea;
  overflow: hidden;
}

.circles {
  inset: 2px; /* = border of .chart-container */
  position: absolute;
  pointer-events: none;
}

.chart-svg {
  height: 100%;
  width: 100%;
}
</style>
