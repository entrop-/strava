<template>
  <div v-if="activitiesByUser">
    <div v-for="(activity, index) in activitiesByUser" :key="`act_${index}`">
      {{ index }}: {{ prettyPrint(activity) }}
    </div>
  </div>
</template>

<script>
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
        const aggregate = result[username] || 0;

        result[username] = aggregate + parseFloat(currentValue.distance);
        return result;
      }, {});
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
