<template>
  <div class="list-container">
    <ul>
      <li
        v-for="spaceship in spaceships"
        :key="spaceship.id"
        @click="itemClick(spaceship)">
        {{ spaceship.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'SpaceshipList',
  props: ['spaceships'],
  methods: {
    itemClick(spaceship) {
      this.$emit('item-click', spaceship.id)
    }
  }
}
</script>

<style scoped>
.list-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 18rem;
  padding: .5rem;
  height: 100%;
  background: #111;
  color: gold;
}

li {
  cursor: pointer;
}
</style>