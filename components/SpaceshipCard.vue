<template>
  <div class="card">
    <p v-if="loading">Loading...</p>
    <p v-else-if="!spaceship && !loading">No spaceship data available</p>
    <div v-else class="card-data">
      <p>Name: {{ spaceship.name }} </p>
      <p>Model: {{ spaceship.model }}</p>
      <p>Manufacturer: {{ spaceship.manufacturer }}</p>
      <p>Cost: {{ spaceship.cost_in_credits }}</p>
      <p>Crew: {{ spaceship.crew }}</p>
      <p>Cargo capacity: {{ spaceship.cargo_capacity }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SpaceshipCard',
  props: ['spaceship', 'loading']
}
</script>

<style scoped>
.card {
  height: 300px;
  width: 500px;
  background: #444;
  color: lightgoldenrodyellow;
  padding: 1.5rem;
}
</style>