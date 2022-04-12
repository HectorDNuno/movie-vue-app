<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Lets see some movies!",
      movies: [],
      newMovieParams: {},
    };
  },
  created: function () {
    axios.get("/movies.json").then((response) => {
      this.movies = response.data;
      console.log("All movies", this.movies);
    });
  },
  methods: {
    addMovie: function () {
      axios
        .post("/movie.json", this.newMovieParams)
        .then((response) => {
          console.log("Movie added!", response.data);
          this.movie.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="addMovie">Add a movie!</button>

    <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
      <br />
      Year:
      <input type="text" v-model="newMovieParams.year" />
      <br />
      Plot:
      <input type="text" v-model="newMovieParams.Plot" />
      <br />
      Director:
      <input type="text" v-model="newMovieParams.director" />
    </div>

    <div v-for="movie in movies" :key="movie.id">
      <p>Title: {{ movie.title }}</p>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
    </div>
  </div>
</template>

<style></style>
