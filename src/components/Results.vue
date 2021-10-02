<template>
  <pre>Strava: {{ activities }}</pre>
</template>

<script>
export default {
  name: "Results",
  props: {
    activities: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped></style>
