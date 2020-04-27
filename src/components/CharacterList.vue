<template lang="html">
  <div v-if="characters" class="">
    <p>Characters</p>
    <hr>
    <character-list-item v-for="(character, index) in characters" :key="index" :character="character"></character-list-item>
  </div>
</template>

<script>
import CharacterListItem from './CharacterListItem.vue'

export default {
  name: 'character-list',
  props: ['characters'],
  components: {
    'character-list-item': CharacterListItem
  }
}
</script>

<style lang="css" scoped>
</style>
