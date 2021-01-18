<template>
  <div class="search">
    <v-container>
      <v-row no-gutters>
        <v-col cols="12">
          <h2>{{ title }}</h2>
          <p>{{ subtitle }}</p>
          <p>{{ examples }}</p>

          <form v-on:submit.prevent="getResult(query)">
            <v-text-field type="text" v-model="query" label="Ingresa una palabra curiosa" />
          </form>
        </v-col>
      </v-row>
      <div v-if="results" class=" d-md-flex">
        <v-card class="d-flex align-content-start flex-wrap justify-center" flat tile>
          <v-card v-for="result in results" :key="result.id" class="pa-2 ma-2" outlined tile>
            <img v-bind:src="result.links[0].href" class="imgs" height="200" />
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
import Swal from "sweetalert2";
export default {
  name: "search",
  data() {
    return {
      title: "¿Qué deseas buscar? ",
      subtitle: "Este es un simple buscador de imágenes de la NASA, sólo debes escribir una palabra para que se realice una búsqueda relacionada a su solicitud. Por el momento sólo se aceptan palabras en Inglés, pero eventualmente se implementará el idioma Español.",
      examples: "Trate de usar palabras clave, como nombres de planetas, galaxias, estrellas, misiones espaciales, astronautas, científicos astrónomos entre otros... Algunos ejemplos:{ Jupiter, Neptune, Moon, Sun, Demo-crew , Apollo 11, Neil Armstrong, Valentina Tereshkova, Elon Musk, Carl Sagan, Andromeda, Quasar } ",
      query: "",
      results: [],
    };
  },
  created() {
    this.getResult("Spacex");
  },
  methods: {
    getResult(query) {
      Swal.fire({
        title: "Un momento por favor",
        text: "Estamos buscando las mejores imágenes",
        onBeforeOpen: () => {
          Swal.showLoading();
        },
      });
      axios.get("https://images-api.nasa.gov/search?q=" + query + "&media_type=image").then((response) => {
        // console.log("getResult -> response", response.data.collection.items);
        this.results = response.data.collection.items;
      });
      Swal.close();
    },
  },
};
</script>
<style scoped>
@media screen and (max-width: 600px) {
  .imgs {
    width: 300px;
    height: auto;
  }
}
</style>
