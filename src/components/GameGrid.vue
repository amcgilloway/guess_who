<template lang="html">
  <v-layout>
    <v-card>
      <v-container
      fluid
      grid-list-md
      >
      <v-layout row wrap>
        <v-flex
        v-for="character in characters"
        :key="character._id"
        v-bind="{ [`xs${character.flex}`]: true }"
        >
        <v-card v-if="!character.guessed"
        hover
        :img="character.url"
        height="300px"
        width="200px"
        color="blue"
        ripple
        @click="handleGuess(character)"
        >
      </v-card>
    </v-flex>
  </v-layout>
</v-container>
</v-card>
</v-flex>
</v-layout>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'game-grid',
  props: ['allCharacters', 'mysteryCharacter'],
  data() {
    return {
      characters: this.allCharacters,
      guessed: false,
      removedCharacters: []
    }
  },
  created() {
    this.characters.forEach((character) => {
      character.url = require('@/assets/avatars/' + character.name + '.png');
      character.guessed = false;
    })
  },
  mounted(){
    eventBus.$on("option-selected", (option) => {
      this.characters.forEach((character) => {
        if(option.remainingChoices){
          if (option.remainingChoices/length >1){
          console.log(character.name, character.hair_colour, option.remainingChoices.includes(character[option.characteristic]));
           if (!option.remainingChoices.includes(character[option.characteristic])){
            this.removeCharacter(character)
          }
        }
        else if (option.remainingChoices.length === 1 && this.mysteryCharacter[option.characteristic] !== character[option.characteristic]) {
            this.removeCharacter(character)
          }
        }
      })

      if(this.characters.length === 1){
        eventBus.$emit('game-won')
      };
    })
  },
  methods: {
    handleGuess: function(character){
      if( character === this.mysteryCharacter ){
        this.characters = [character]
        eventBus.$emit('game-won')
      } else {
        this.removeCharacter(character)
      }
    },
    removeCharacter: function(guessedCharacter){
      // guessedCharacter.guessed = true;
      this.characters = this.characters.filter( function( character ) {
        return guessedCharacter.name !== character.name;
      } );
    }
  }
}
</script>

<style lang="css" scoped>
.mystery-character {
  height: 25vh;
  width: 15vw;
}
</style>
