<template>
  <div class="home">
    <SearchObjectSpace></SearchObjectSpace>
  </div>
</template>

<script>
// @ is an alias to /src
import SearchObjectSpace from "@/components/SearchObjectSpace.vue";

export default {
  name: "Home",
  components: {
    SearchObjectSpace,
  },
};
</script>
