<template lang="html">
  <v-navigation-drawer
  fixed
  app
  permanent
  >
  <div class="text-xs-center">
    <h3>Choose an option below</h3>
    <v-menu v-for="key in Object.keys(choices)" offset-y>
      <template v-if="key !== '_id' && key === 'Hair Colour' || key === 'Eye Colour'" v-slot:activator="{ on }">
        <v-btn
        color="primary"
        dark
        v-on="on"
        :id="key.substring(0, 3)"
        >
        {{key}}?
        <v-icon>arrow_drop_down</v-icon>
      </v-btn>
    </template>

    <v-list>
      <v-list-tile
      v-for="(choice, index) in choices[key]"
      :key="index"
      @click="handleChoice(key, choice)"
      >
      <v-list-tile-title>{{ choice }}</v-list-tile-title>
    </v-list-tile>
  </v-list>
</v-menu>
<v-menu v-for="key in Object.keys(choices)" offset-y>
  <template v-if="key !== '_id' && key !== 'Hair Colour' && key !== 'Eye Colour'" v-slot:activator="{ on }">
    <v-btn
    color="primary"
    dark
    v-on="on"
    @click="handleTrueFalseChoice(key)"
    :id="key.substring(key.length - 3)"
    :value="true"
    >
    {{key}}?
  </v-btn>
</template>

</v-menu>

</div>
</v-navigation-drawer>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'sidebar',
  props: ['choices'],
  methods: {
    handleChoice: function(key, choice){
      const selected = {}
      selected.characteristic = key.toLowerCase().replace(" ", "_");
      selected.value = choice;
      selected.remainingChoices = null;
      this.choices[key].splice(this.choices[key].indexOf(choice), 1)
      if(this.choices[key].length ===1){
        const button = document.querySelector(`#${key.substring(0, 3)}`)
        button.classList.add('hidden')
      }
      if(this.choices[key].length > 1){
        selected.remainingChoices = this.choices[key]
      }
      eventBus.$emit('option-selected', selected);
    },
    handleTrueFalseChoice: function(key){
      const selected = {}
      selected.characteristic = key.toLowerCase().replace(" ", "_");
      selected.value = true
      this.removeButton(key)
      eventBus.$emit('option-selected', selected);
    },
    removeButton: function(key){
      const button = document.querySelector(`#${key.substring(key.length -3)}`)
      button.classList.add('hidden')
    }
  }

}
</script>

<style lang="css" scoped>
.hidden {
  display: none;
}
</style>
