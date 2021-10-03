<template>
  <h1>Antologic challenge</h1>
  <div class="flex flex-row">
    <Club
      :club-id="runId"
      class="w-1/2"
      club-name="Bieganko"
      :config="config"
    />
    <Club
      :club-id="bikeId"
      class="w-1/2"
      club-name="Rowerek"
      :config="config"
    />
  </div>
</template>

<script>
import Club from "@/components/Club";

export default {
  name: "Home",
  components: {
    Club,
  },
  data() {
    return {
      runId: process.env.VUE_APP_STRAVA_CLUB_RUN_ID,
      bikeId: process.env.VUE_APP_STRAVA_CLUB_BIKE_ID,
      config: {
        access_token: process.env.VUE_APP_STRAVA_TOKEN,
        client_id: process.env.VUE_APP_STRAVA_CLIENT_ID,
        client_secret: process.env.VUE_APP_STRAVA_CLIENT_SECRET,
        redirect_uri: process.env.VUE_APP_STRAVA_REDIRECT_URI,
      },
    };
  },
};
</script>

<style lang="scss"></style>
