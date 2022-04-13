<script>
import axios from "axios";

// import axios from "axios";
export default {
  data: function () {
    return {
      currentMovie: {},
    };
  },
  created: function () {
    axios.get("/movie/" + this.$route.params.id + ".json").then((response) => {
      console.log("movies show", response);
      this.currentMovie = response.data;
    });
  },
};
</script>

<template>
  <div class="movies-show">
    <h4>{{ currentMovie.title }}</h4>
    <p>{{ currentMovie.year }}</p>
    <p>{{ currentMovie.plot }}</p>
    <p>{{ currentMovie.director }}</p>
    <a href="/movies">back to all movies</a>
    |
    <a :href="`/movies/edit/${currentMovie.id}`">edit movie</a>
  </div>
</template>
