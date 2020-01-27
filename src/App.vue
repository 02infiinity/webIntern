<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
       <span class="mr-2 title font-weight-white white--text">WEB TRANSLITERATION</span>
      </div>

      <v-spacer></v-spacer>

     
      <template>

    <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
      <template v-slot:activator="{ on }">
        <v-btn color="primary" dark v-on="on">
          <span class=" mr-2 hidden-sm-and-down">How To Use</span>
          <i class="material-icons">
info
</i>
</v-btn>
      </template>
      <v-card>
        <v-toolbar dark color="primary">
         
          <v-toolbar-title><span class="font-weight-light white--text">HOW TO USE </span><span class="mr-2 title font-weight-white white--text"> WEB TRANSLITERATION</span> </v-toolbar-title>
          <v-spacer></v-spacer>

               <v-btn color="primary mx-2" dark @click="dialog = false">
          <span class=" mr-2 hidden-sm-and-down">Close</span>
            <v-icon>mdi-close</v-icon>
          </v-btn>
 
        </v-toolbar>
        <v-container>
        <v-card-title>
          <span class="headline">Step 1:</span>
        </v-card-title>
        <v-card-text>
          First choose language in which you want TRANSLITERATION.
         </v-card-text>
          <v-card-title>
          <span class="headline">Step 2:</span>
        </v-card-title>
        <v-card-text>
          Start writing text in textbox (In enlish language).
         </v-card-text>
          <v-card-title>
          <span class="headline">Step 3:</span>
        </v-card-title>
        <v-card-text>
          As you start typing there will be a dropdown list apper witch contain the TRANSLITERATION suggestion.
          Select the option from list to change the english word to your favourite language.
         </v-card-text>
        </v-container>
      </v-card>
    </v-dialog>

</template>
    </v-app-bar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

   data () {
      return {
        dialog: false,
        notifications: false,
        sound: true,
        widgets: false,
      }
    },
};
</script>
