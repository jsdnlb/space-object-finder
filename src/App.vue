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
      <h2 class="d-md-flex d-none xs">Search for space objects</h2>

      <v-spacer></v-spacer>

      <h4>
        Developed by: <a href="https://github.com/jsdnlb">Daniel Buitrago</a>
      </h4>
    </v-app-bar>

    <v-content>
      <SearchObjectSpace />
    </v-content>
  </v-app>
</template>
<style scoped>
h4, a{
  color: white !important;
  text-decoration: none;
}
</style>
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
