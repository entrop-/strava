<template>
  <Members v-if="members" :members="members" />
  <Results v-if="stravaData" :strava-data="stravaData" />
</template>

<script>
import Results from "@/components/Results";
import strava from "strava-v3";
import Members from "@/components/Members";

export default {
  name: "Home",
  components: {
    Members,
    Results,
  },
  mounted() {
    this.fetchStravaData();
  },
  methods: {
    async fetchStravaData() {
      this.members = await strava.clubs.listMembers({
        id: process.env.VUE_APP_STRAVA_CLUB_ID,
        ...this.config,
      });

      // this.stravaData = await strava.athlete.listClubs({
      //   id: config.client_id,
      //   ...config
      // });
    },
  },
  data() {
    return {
      config: {
        access_token: process.env.VUE_APP_STRAVA_TOKEN,
        client_id: process.env.VUE_APP_STRAVA_CLIENT_ID,
        client_secret: process.env.VUE_APP_STRAVA_CLIENT_SECRET,
        redirect_uri: process.env.VUE_APP_STRAVA_REDIRECT_URI,
      },
      stravaData: null,
      members: [],
    };
  },
};
</script>

<style lang="scss"></style>
