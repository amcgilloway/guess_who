<template lang="html">
  <v-flex xs12 sm6 offset-sm5  class="mystery-character">
    <h1 v-if="guessed">You Guessed {{mysteryCharacter.name}} correctly!</h1>
      <v-card
      hover
      :img="guessed? url : hiddenUrl"
      height="200px"
      width="150px"
      ripple
      @click="guessed = true"
      >
      </v-card>
    </v-flex>
</template>

<script>

import {eventBus} from '../main.js';

export default {
  name: 'mystery-card',
  props: ['mysteryCharacter'],
  data() {
    return {
      guessed: false,
      hiddenUrl: require('@/assets/avatars/question_mark.jpg'),
      url: require('@/assets/avatars/' + this.mysteryCharacter.name + '.png')
    }
  },
  mounted(){
    eventBus.$on('game-won', () => {
      this.guessed = true
    })
  }
}
</script>

<style lang="css" scoped>
.mystery-character {
  height: 25vh;
  width: 15vw;
  margin-bottom:100px;
}
</style>
