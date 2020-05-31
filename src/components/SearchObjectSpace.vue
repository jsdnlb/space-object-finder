<template>
  <div class="search">
    <v-container>
      <v-row no-gutters>
        <v-col cols="12">
          <h2>{{ title }}</h2>
          <p>{{ subtitle }}</p>

          <form v-on:submit.prevent="getResult(query)">
            <v-text-field type="text" v-model="query" />
          </form>
        </v-col>
      </v-row>
      <div v-if="results">
        <v-card
          class="d-flex align-content-start flex-wrap"
          flat
          tile
          min-height="200"
        >
          <v-card
            v-for="result in results"
            :key="result.id"
            class="pa-2"
            outlined
            tile
          >
            <img v-bind:src="result.links[0].href" height="200" />
          </v-card>
        </v-card>
      </div>
      <div v-if="results.length == 0">
        <h1>No se enontraron resultados relacionados con la búsqueda.</h1>
      </div>
    </v-container>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "search",
  data() {
    return {
      title: "¿Qué deseas buscar? ",
      subtitle:
        "Este es un simple buscador de imágenes de la NASA, sólo debes escribir una palabra para que se realice una búsqueda relacionada a su solicitud. Por el momento sólo se aceptan palabras en Inglés, pero enventualmente se implementará el idioma Español.",
      query: "",
      results: [],
    };
  },
  methods: {
    getResult(query) {
      axios
        .get(
          "https://images-api.nasa.gov/search?q=" + query + "&media_type=image"
        )
        .then((response) => {
          console.log("getResult -> response", response.data.collection.items);
          this.results = response.data.collection.items;
        });
    },
  },
};
</script>
