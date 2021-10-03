<template>
  <div class="w-1/2">
    <h2>{{ clubName }}</h2>
    <Results v-if="activities" :activities="activities" :members="members" />
    <Members v-if="members" :members="members" />
  </div>
</template>

<script>
import strava from "strava-v3";
import Members from "@/components/Members";
import Results from "@/components/Results";
// import axios from "axios";

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
      // this.members = await strava.clubs.listMembers({
      //   id: this.clubId,
      //   ...this.config,
      // });

      const today = new Date();
      const first =
        new Date(today.getFullYear(), today.getMonth(), 1).getTime() / 1000;

      // this.activities = await axios.get(
      //   `https://www.strava.com/api/v3/clubs/${this.clubId}/activities?after=${first}`,
      //   { ...this.config },
      //   {
      //     headers: {
      //       Authorization: `Bearer ${this.config.access_token}`,
      //     },
      //   }
      // );
      // console.log(this.activities);
      this.activities = await strava.clubs.listActivities({
        id: this.clubId,
        after: first,
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
