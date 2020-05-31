<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />
        <h2>Search Object in Space</h2>
      </div>

      <v-spacer></v-spacer>

      <h4>Developed by: Daniel Buitrago</h4>
    </v-app-bar>

    <v-content>
      <SearchObjectSpace />
    </v-content>
  </v-app>
</template>

<script>
import SearchObjectSpace from "./components/SearchObjectSpace";

export default {
  name: "App",

  components: {
    SearchObjectSpace,
  },

  data: () => ({
    //
  }),
};
</script>
