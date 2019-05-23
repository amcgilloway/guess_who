<template lang="html">
  <v-toolbar color="indigo" dark fixed app>
    <v-toolbar-title>Guess Who</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
      <template v-slot:activator="{ on }">
        <v-btn color="indigo" dark v-on="on">How to play</v-btn>
      </template>
      <v-card>
        <v-toolbar dark color="indigo">
          <v-btn icon dark @click="dialog = false">
            <v-icon>close</v-icon>
          </v-btn>
          <v-toolbar-title>How to Play</v-toolbar-title>
          <v-spacer></v-spacer>

        </v-toolbar>
        <v-list three-line subheader>
          <v-subheader>Rules</v-subheader>
          <v-list-tile avatar>
            <v-list-tile-content>
              <v-list-tile-title>Aim of the game</v-list-tile-title>
              <v-list-tile-sub-title>Guess Who is a game where players use yes or no questions to isolate a hidden character. Once the player guesses the hidden character they win.</v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile avatar>
            <v-list-tile-content>
              <v-list-tile-title>Guessing a characteristic</v-list-tile-title>
              <v-list-tile-sub-title>On the left hand side there are buttons for different characteristics. <br>Once you click the characteristic if the mystery character doesn't have that characteristic then those characters cards are removed from game area. </v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile avatar>
            <v-list-tile-content>
              <v-list-tile-title>Guessing a character</v-list-tile-title>
              <v-list-tile-sub-title>Click on a player card to guess that character. If it isn't that character then that card is removed from play</v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
        <v-divider></v-divider>
      </v-card>
    </v-dialog>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
  data () {
      return {
        dialog: false,
        notifications: false,
        sound: true,
        widgets: false
      }
    }
}
</script>

<style lang="css" scoped>
</style>
