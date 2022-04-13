<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("/movie/" + this.$route.params.id + ".json").then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      axios.patch("/movie/" + this.$route.params.id + ".json", this.movie).then((response) => {
        console.log("movies updated", response.data);
        this.$router.push("/movies");
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
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Update Movie!</h1>

      <div>
        <div class="form-group">
          title:
          <input type="text" v-model="movie.title" />
        </div>
        <div class="form-group">
          year:
          <input type="text" v-model="movie.year" />
        </div>
        <div class="form-group">
          plot:
          <input type="text" v-model="movie.plot" />
        </div>
        <div class="form-group">
          director:
          <input type="text" v-model="movie.director" />
        </div>
      </div>
      <input type="submit" value="update" />
      <button v-on:click="destroyMovie(movie)">delete</button>
      <br />
      <a href="/movies">back to all movies</a>
    </form>
  </div>
</template>
