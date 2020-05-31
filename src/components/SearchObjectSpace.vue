<template>
  <div class="search">
    <h1>{{ title }}</h1>
    <h2>{{ msg }}</h2>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" v-model="query" />
    </form>
    <div v-if="results">
      <div v-for="result in results" :key="result.id">
        <img v-bind:src="result.links[0].href" />
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "search",
  data() {
    return {
      title: "Search Objet in Space",
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
