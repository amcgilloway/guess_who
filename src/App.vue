<template>
  <v-app id="inspire">
    <SideBar v-if="choices.length > 0" :choices="choices[0]" />
    <Header />
    <GuessWhoView v-if="characters.length > 1" :characters="characters" />
  </v-app>
</template>

<script>

import SideBar from './components/SideBar';
import Header from './components/Header';
import guessWhoService from './services/GuessWhoService';
import GuessWhoView from './views/GuessWhoView';

  export default {
    name: 'App',
    data: () => ({
      drawer: null,
      choices: [],
      characters: []
    }),
    components: {
      SideBar,
      Header,
      GuessWhoView
    },
    mounted(){
      const baseUrl = 'https://codeclan-guess-who.herokuapp.com/'
      guessWhoService.getData( baseUrl + 'api/characters')
      .then(characters => this.characters = characters)
      guessWhoService.getData(baseUrl + 'api/choices')
      .then(choices => this.choices = choices)

    }

  }
</script>
