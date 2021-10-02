<template>
  <div class="w-1/2">
    <h2>{{ clubName }}</h2>
    <Results :activities="activities" />
    <Members v-if="members" :members="members" />
  </div>
</template>

<script>
import strava from "strava-v3";
import Members from "@/components/Members";
import Results from "@/components/Results";

export default {
  name: "Club",
  components: { Results, Members },
  props: {
    clubName: {
      type: String,
      default: null,
    },
    clubId: {
      type: String,
      default: null,
    },
    config: {
      type: Object,
      default: () => {},
    },
  },
  mounted() {
    this.fetchStravaData();
  },
  methods: {
    async fetchStravaData() {
      this.members = await strava.clubs.listMembers({
        id: this.clubId,
        ...this.config,
      });
    },
  },
  data() {
    return {
      members: [],
      activities: [],
    };
  },
};
</script>

<style scoped></style>
