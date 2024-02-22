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
      v-for="(item, index) in items"
      :key="item.id"
      :index="index"
      :count="items.length"
      :chartAngle="chartAngle"
    >
      <div class="item-circle-content-wrapper">
        <img class="item-circle-icon" :src="item.iconPath" />

        <div v-if="item.haveWarning" class="item-circle-warning">
          <img src="/icons/warning.svg" />
        </div>
      </div>
    </item-circle>
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
        {
          id: 1,
          value: 100,
          title: "Эндокринная система",
          iconPath: "/icons/endocrine.svg",
          haveWarning: false,
        },
        {
          id: 2,
          value: 100,
          title: "Репродуктивная система",
          iconPath: "/icons/reproductive.svg",
          haveWarning: false,
        },
        {
          id: 3,
          value: 80,
          title: "Мочевыделительная система",
          iconPath: "/icons/urinary.svg",
          haveWarning: false,
        },
        {
          id: 4,
          value: 60,
          title: "Пищеварительная система",
          iconPath: "/icons/digestion.svg",
          haveWarning: false,
        },
        {
          id: 5,
          value: 100,
          title: "Дыхательная система",
          iconPath: "/icons/lungs.svg",
          haveWarning: false,
        },

        {
          id: 6,
          value: 80,
          title: "Опорно-двигательная система",
          iconPath: "/icons/musculoskeletal.svg",
          haveWarning: false,
        },
        {
          id: 7,
          value: 40,
          title: "Кроветворная и иуммунная система",
          iconPath: "/icons/immune.svg",
          haveWarning: true,
        },
        {
          id: 8,
          value: 60,
          title: "Лимфатическая система",
          iconPath: "/icons/lymphatic.svg",
          haveWarning: false,
        },

        {
          id: 9,
          value: 40,
          title: "Сердечно-сосудистая система",
          iconPath: "/icons/cardiovascular.svg",
          haveWarning: true,
        },

        {
          id: 10,
          value: 80,
          title: "Покровная система",
          iconPath: "/icons/integumentary.svg",
          haveWarning: false,
        },
        {
          id: 11,
          value: 60,
          title: "Нервная система",
          iconPath: "/icons/nervous.svg",
          haveWarning: false,
        },
        {
          id: 12,
          value: 80,
          title: "Система органов чувств",
          iconPath: "/icons/sense-organs.svg",
          haveWarning: false,
        },
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

.item-circle-content-wrapper {
  position: relative;
}

.item-circle-content-wrapper:hover {
  opacity: 0.7;
}

.item-circle-warning {
  position: absolute;
  right: -5px;
  bottom: -5px;

  height: 25px;
  width: 25px;

  background-color: #ff5300;

  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 100%;

  box-shadow: 0 5px 5px 0 rgba(0, 0, 0, 0.25);
}

.item-circle-warning > img {
  height: 100%;
  width: 100%;
  padding: 6px;
}

.item-circle-icon {
  height: 100%;
  width: 100%;
  padding: 8px;
}
</style>
