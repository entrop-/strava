<template>
  <div v-if="activitiesByUser">
    <div v-for="(activity, index) in sortedScores" :key="`act_${index}`">
      {{ activity.name }}: {{ prettyPrint(activity.distance) }}
    </div>
  </div>
</template>

<script>
import { orderBy } from "lodash";
export default {
  name: "Results",
  props: {
    activities: {
      type: Array,
      default: () => [],
    },
    members: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    activitiesByUser() {
      return this.activities.reduce((result, currentValue) => {
        const username =
          currentValue.athlete.firstname + " " + currentValue.athlete.lastname;
        const entry = result.findIndex(
          (activity) => activity.name === username
        );
        const aggregate = result[entry]?.distance || 0;

        const data = {
          name: username,
          distance: aggregate + parseFloat(currentValue.distance),
        };
        if (entry < 0) result.push(data);
        else result[entry] = data;
        return result;
      }, []);
    },
    sortedScores() {
      return orderBy(this.activitiesByUser, "distance", "desc");
    },
  },
  methods: {
    prettyPrint(value) {
      return (value / 1000).toFixed(1) + " km";
    },
  },
};
</script>

<style scoped></style>
