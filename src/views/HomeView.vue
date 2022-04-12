<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Lets see some movies!",
      movies: [],
      newMovieParams: {},
      currentMovie: {},
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
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-info").showModal();
    },
    updateMovie: function (movie) {
      var updateMovieParams = movie;
      axios.patch("/movie/" + movie.id + ".json", updateMovieParams).then((response) => {
        console.log("Updated!", response.data);
      });
    },
    destroyMovie: function (movie) {
      axios.delete("/movie/" + movie.id).then((response) => {
        console.log("Deleted!", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>

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

    <button v-on:click="addMovie">Add movie!</button>

    <div v-for="movie in movies" :key="movie.id">
      <p>Title: {{ movie.title }}</p>
      <p>Year: {{ movie.year }}</p>
      <!-- <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p> -->
      <button v-on:click="showMovie(movie)">See More</button>
    </div>

    <dialog id="movie-info">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>
          Title:
          <input type="text" v-model="currentMovie.title" />
        </p>
        <p>
          Year:
          <input type="text" v-model="currentMovie.year" />
        </p>
        <p>
          Plot:
          <input type="text" v-model="currentMovie.plot" />
        </p>
        <p>
          Director:
          <input type="text" v-model="currentMovie.director" />
        </p>
        <button>Close</button>
        <button v-on:click="updateMovie(currentMovie)">Edit</button>
        <button v-on:click="destroyMovie(currentMovie)">Destroy</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>
