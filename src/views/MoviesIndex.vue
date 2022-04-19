<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      message: "Lets see some movies!",
      movies: [],
      titleFilter: "",
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
    Search by title:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" :key="movie.id">{{ movie.title }}</option>
    </datalist>
    <div v-for="movie in filterBy(movies, titleFilter, 'title')" :key="movie.id">
      <h4>{{ movie.title }}</h4>
      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <p>{{ movie.director }}</p>
      <a :href="`/movies/show/${movie.id}`">Go to movie page</a>
    </div>
  </div>
</template>
