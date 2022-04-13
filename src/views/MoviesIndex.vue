<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Lets see some movies!",
      movies: [],
    };
  },
  created: function () {
    axios.get("/movies.json").then((response) => {
      console.log("all movies", response);
      this.movies = response.data;
    });
  },
};
</script>

<template>
  <div class="movies-index">
    <div v-for="movie in movies" :key="movie.id">
      <h4>{{ movie.title }}</h4>
      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <p>{{ movie.director }}</p>
      <a :href="`/movies/show/${movie.id}`">Go to movie page</a>
    </div>
  </div>
</template>
