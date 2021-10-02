<template>
  <pre>{{ members }}</pre>
  <ul>
    <li v-for="(member, index) in members" :key="`mem_${index}`">
      {{ member.firstname }}, {{ member.lastname }}
    </li>
  </ul>
</template>

<script>
import strava from "strava-v3";

export default {
  name: "Members",
  props: {
    members: {
      type: Array,
      default: () => [],
    },
  },
  mounted() {
    this.getStats();
  },
  methods: {
    async getStats() {
      const today = new Date();
      const first =
        new Date(today.getFullYear(), today.getMonth(), 1).getTime() / 1000;

      this.memberList = this.members.map(async (member) => {
        return await strava.athletes.stats({
          id: member.id,
          after: first,
          ...this.config,
        });
      });
    },
  },
  data() {
    return {
      memberList: [],
    };
  },
};
</script>

<style scoped></style>
