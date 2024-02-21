<template>
  <path
    :d="pathData"
    stroke-width="2"
    stroke="white"
    class="triangle"
    :class="[{ active: isAcitve }, fillClass]"
    @click="$emit('click')"
  />
</template>

<script>
export default {
  emits: ["click"],

  props: {
    index: Number,
    itemValue: Number,
    numTriangles: Number,
    activeTriangleIndex: Number,
  },

  data() {
    return {
      wrapperHeight: 0,
    };
  },

  computed: {
    fillClass() {
      return "triangle-" + this.itemValue;
    },

    isAcitve() {
      return this.activeTriangleIndex == this.index;
    },

    pathData() {
      const chartRadius = this.wrapperHeight / 2;
      const angle = ((Math.PI * 2) / this.numTriangles) * this.index;
      const heightСoefficient =
        this.wrapperHeight - (this.wrapperHeight * this.itemValue) / 100;

      const triangle = document.createElementNS(
        "http://www.w3.org/2000/svg",
        "path"
      );
      const x1 =
        chartRadius + Math.cos(angle) * (chartRadius - heightСoefficient / 2);
      const y1 =
        chartRadius + Math.sin(angle) * (chartRadius - heightСoefficient / 2);

      const x2 =
        chartRadius +
        Math.cos(angle + (Math.PI * 2) / this.numTriangles) *
          (chartRadius - heightСoefficient / 2);
      const y2 =
        chartRadius +
        Math.sin(angle + (Math.PI * 2) / this.numTriangles) *
          (chartRadius - heightСoefficient / 2);

      const _COEFFS = {
        0: 0,
        20: 0.22,
        40: 0.42,
        60: 0.62,
        80: 0.82,
        100: 1.03,
      };
      const _COEFF = _COEFFS[this.itemValue];
      // для создания закругления (нужно подобрать коэффициент, притом разный для каждого value (20,40,60,80,100))
      const controlPointX =
        chartRadius +
        Math.cos(angle + Math.PI / this.numTriangles) * chartRadius * _COEFF;
      const controlPointY =
        chartRadius +
        Math.sin(angle + Math.PI / this.numTriangles) * chartRadius * _COEFF;

      const pathData = `M ${chartRadius},${chartRadius} L ${x1},${y1} Q ${controlPointX},${controlPointY} ${x2},${y2} Z`;

      // const pathData = `M ${chartRadius},${chartRadius} L ${x1},${y1} L ${x2},${y2} Z`;

      return pathData;
    },
  },

  mounted() {
    this.wrapperHeight = this.$el?.parentNode.clientHeight;
  },
};
</script>

<style scoped>
.active {
  fill: blue !important;
}

.triangle {
  cursor: pointer;
}

.triangle-20 {
  fill: #ed948e;
}

.triangle-40 {
  fill: #ed948e;
}

.triangle-60 {
  fill: #f2d47c;
}

.triangle-80 {
  fill: #76e2c7;
}

.triangle-100 {
  fill: #80b973;
}

.triangle:hover {
  opacity: 0.7;
}
</style>
