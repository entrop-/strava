<template>
  <ul>
    <li v-for="member in members" :key="member.id">{{ member.name }}</li>
  </ul>
</template>

<script>
export default {
  name: "Members",
  props: {
    members: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped></style>
