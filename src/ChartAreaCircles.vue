<template>
  <svg viewBox="0 0 200 200" class="circles">
    <circle
      v-for="value in circlesValues"
      :key="value"
      cx="100"
      cy="100"
      :r="value"
      fill="none"
      stroke="white"
      stroke-width="1"
    />
  </svg>
</template>

<script>
export default {
  props: {
    circlesValues: Array,
  },
};
</script>
