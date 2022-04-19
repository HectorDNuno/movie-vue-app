<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Add a movie!",
      movies: [],
      newMovieParams: { plot: "" },
    };
  },
  methods: {
    createMovie: function () {
      axios.post("/movie.json", this.newMovieParams).then((response) => {
        console.log("movie added", response.data);
        this.movies.push(response.data);
        this.$router.push("/movies");
      });
    },
  },
};
</script>

<template>
  <div class="create-movies">
    <div>
      <p>
        Title:
        <input type="text" v-model="newMovieParams.title" />
      </p>
      <p>
        Year:
        <input type="text" v-model="newMovieParams.year" />
      </p>
      <p>
        Plot:
        <input type="text" v-model="newMovieParams.plot" />
        <small v-if="newMovieParams.plot.length > 100">Plot is too long!</small>
      </p>
      <p>
        Director:
        <input type="text" v-model="newMovieParams.director" />
      </p>
      <button v-on:click="createMovie()">Add!</button>
    </div>
  </div>
</template>
