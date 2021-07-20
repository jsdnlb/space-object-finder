<template>
  <div class="search">
    <v-container>
      <v-row no-gutters>
        <v-col cols="12">
          <h2>{{ title }}</h2>
          <p>{{ subtitle }}</p>
          <p>{{ examples }}</p>

          <form v-on:submit.prevent="getResult(query)">
            <v-text-field
              type="text"
              v-model="query"
              label="Enter a curious word"
            />
          </form>
        </v-col>
      </v-row>
      <div v-if="results" class="d-md-flex">
        <v-card
          class="d-flex align-content-start flex-wrap justify-center"
          flat
          tile
        >
          <v-card
            v-for="result in results"
            :key="result.id"
            class="pa-2 ma-2"
            outlined
            tile
          >
            <img v-bind:src="result.links[0].href" class="imgs" height="200" />
          </v-card>
        </v-card>
      </div>
      <div v-if="results.length == 0">
        <h1>No results related to the search were found.</h1>
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
      title: "What do you want to search for?",
      subtitle:
        "Try to use keywords, such as names of planets, galaxies, stars, space missions, astronauts, astronomer scientists among others... Some examples:[Jupiter, Neptune, Moon, Sun, Demo-crew , Apollo 11, Neil Armstrong, Valentina Tereshkova, Elon Musk, Carl Sagan, Andromeda, Quasar]",
      examples: "",
      query: "",
      results: [],
    };
  },
  created() {
    this.getResult("X");
  },
  methods: {
    getResult(query) {
      Swal.fire({
        title: "One moment please",
        text: "We are looking for the best images",
        onBeforeOpen: () => {
          Swal.showLoading();
        },
      });
      axios
        .get(
          "https://images-api.nasa.gov/search?q=" + query + "&media_type=image"
        )
        .then((response) => {
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
