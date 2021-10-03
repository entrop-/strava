<template>
  <ul>
    <li v-for="(member, index) in members" :key="`mem_${index}`">
      {{ member.firstname }}, {{ member.lastname }}
    </li>
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
