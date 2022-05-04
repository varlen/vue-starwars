  <!-- Please remove this file from your project -->
<template>
  <div class="relative flex items-top justify-center min-h-screen sm:items-center sm:pt-0 bg">
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css" rel="stylesheet">
    <div>
      <h1>Star Wars Spaceship #{{ currentSpaceshipIndex }}</h1>
      <SpaceshipCard
        :spaceship="currentSpaceshipData"
        :loading="isLoading"
      />
      <input
        class="golden-black-input"
        type="number"
        min="2"
        v-model="currentSpaceshipIndex"
      />
      <SpaceshipList
        :spaceships="mySpaceships"
        @item-click="currentSpaceshipIndex = $event"
      />
      <b-button
      class="right"
      :disabled="!this.currentSpaceshipData"
      @click="addFavourite()">Add</b-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NuxtTutorial',
  data() {
    return {
      currentSpaceshipIndex: 2,
      currentSpaceshipData : null,
      isLoading: false,
      mySpaceships : []
    }
  },
  beforeMount() {
    this.loadSpaceshipData(this.currentSpaceshipIndex)
  },
  methods: {
    loadSpaceshipData(index) {
      this.isLoading = true
      this.$axios.get(`https://swapi.dev/api/starships/${index}/`)
        .then(({data}) => {
          this.currentSpaceshipData = { ...data, id : index }
        })
        .catch(() => {
          this.currentSpaceshipData = null
        })
        .finally(
          () => { this.isLoading = false }
        )
    },
    addFavourite() {
      const containsCurrent = this.mySpaceships.some((s) => s.id == this.currentSpaceshipIndex)
      if (!containsCurrent) {
        this.mySpaceships.push(this.currentSpaceshipData)
      }
    }
  },
  watch: {
    currentSpaceshipIndex : function(newValue) {
      this.loadSpaceshipData(newValue)
    }
  }
}
</script>

<style scoped>
.bg {
  background: #333;
}

.right {
  float: right;
}

h1 {
  color: gold;
  font-size: smaller;
  border-radius: 20px 20px 0px 0px;
  background-color: #444;
  padding-left: 1rem;
  padding-bottom: .5rem;
  padding-top: .5rem;
}

.golden-black-input {
  background: #444;
  color: gold;
  outline-color: gold;
  outline-style: solid;
  outline-width: thin;
  margin: .5rem;
  padding-left: .5rem;
}
</style>
