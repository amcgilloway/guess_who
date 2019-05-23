<template lang="html">
  <v-content>
        <v-flex text-xs-center>
          <MysteryCard v-if="mysteryCharacter" :mysteryCharacter="mysteryCharacter"/>
        </v-flex>
        <v-layout
          justify-center
          align-center
        >
          <v-flex text-xs-center>
          <GameGrid v-if="characters" :allCharacters="characters" :mysteryCharacter="mysteryCharacter" />
        </v-flex>
      </v-layout>
  </v-content>
</template>

<script>

import {eventBus} from "../main.js"
import MysteryCard from '../components/MysteryCard';
import GameGrid from '../components/GameGrid';

export default {
  name: 'guess-who',
  data() {
    return {
      mysteryCharacter: this.characters[Math.floor(Math.random()*this.characters.length)]
    }
  },
  props: ['characters'],
  components: {
    MysteryCard,
    GameGrid
  }
}
</script>

<style lang="css" scoped>
</style>
