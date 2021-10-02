<template>
  <div>Strava: {{ $props }}</div>
</template>

<script>
export default {
  name: "Results",
  props: {
    stravaData: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style scoped></style>
