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
      this.movies = response.data;
      console.log("All movies", this.movies);
    });
  },
  methods: {},
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" :key="movie.id">
      <p>Title: {{ movie.title }}</p>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
    </div>
  </div>
</template>

<style></style>
