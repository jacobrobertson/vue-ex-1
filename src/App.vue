<template>
  <v-app>
    <v-app-bar
      app
      color="blue-grey accent-5"
      dark
      prominent
      fill-height
    >
      <div class="d-flex align-center">
        <v-img
          align="center"
          alt="Tapir Logo"
          src="./assets/tapir-logo-small.png"
          transition="scale-transition"
        />
        <v-divider
          class="mx-4"
          vertical
        ></v-divider>
        <v-toolbar-title align="center" class="display-2">TaPiR - the TFT Personal Recommender</v-toolbar-title>
      </div>
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

  data: () => ({
    //
  }),
};
</script>
