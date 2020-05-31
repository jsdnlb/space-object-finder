<template>
  <div class="search">
    <v-container>
      <v-row no-gutters>
        <v-col cols="12">
          <h2>{{ msg }}</h2>
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
    </v-container>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "search",
  data() {
    return {
      msg: "¿Qué deseas buscar? ",
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
          //   console.log("getResult -> response", response.data.collection.items);
          this.results = response.data.collection.items;
        });
    },
  },
};
</script>
