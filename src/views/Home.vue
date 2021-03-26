<template>
  <div class="home">
    <h1>{{ message }}</h1>
  </div>
  <div v-for="movie in movies" v-bind:key="movie.id">
    <h3>{{ movies.title }}</h3>
  </div>
</template>
<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to The Best Movie App Ever!",
      movies: [],
    };
  },
  created: function () {},
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log("all movies:", this.movies);
      });
    },
    createdMovies: function () {
      this.indexMovies();
    },
  },
};
</script>
