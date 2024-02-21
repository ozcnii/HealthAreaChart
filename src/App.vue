<template>
  <div>
    <health-area-chart class="center" />
  </div>
</template>

<script>
import HealthAreaChart from "./HealthAreaChart.vue";

export default {
  components: { HealthAreaChart },
};
</script>

<style scoped>
.center {
  margin: 50px auto;
}
</style>
