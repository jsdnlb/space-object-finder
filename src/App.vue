<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://upload.wikimedia.org/wikipedia/commons/e/e5/NASA_logo.svg"
          transition="scale-transition"
          width="50"
          @click="reloadPage()"
        />
      </div>
      <h2 class="d-md-flex d-none xs">Búsqueda de objetos espaciales</h2>

      <v-spacer></v-spacer>

      <h4>Desarrollado por: Daniel Buitrago</h4>
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
  methods: {
    reloadPage() {
      window.scrollTo(0, 0);
      location.reload();
    },
  },
};
</script>
