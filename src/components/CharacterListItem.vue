<template lang="html">
  <div class="">
    <p>Name: {{character.name}} - Height: {{character.height | centimetersToMeters}} - Homeworld: {{this.homeworld.name}} - Terrain: {{this.homeworld.terrain}}</p>
  </div>
</template>

<script>
export default {
  name: 'character-list-item',
  props: ['character'],
  filters: {
    centimetersToMeters: function(num) {
      return (num * 0.01).toFixed(2) + "m"
    }
  },
  data() {
    return {
      homeworld: []
    }
  },
  methods: {

  },
  mounted() {
    fetch(this.character.homeworld)
    .then(res => res.json())
    .then(data => this.homeworld = data)
  },
  watch: {

  }
}
</script>

<style lang="css" scoped>
</style>
