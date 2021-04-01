// All movies are not showing online
<template>
  <div class="movies-index">
    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <router-link v-bind:to="`movies/${movie.id}`">
          <h3>{{ movie.title }}</h3>
          <p>{{ movie.user }}</p>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    // the notes say : In <script> created: 	Make a GET request to "/api/photos"
    // get."/api/movies"
    // the reference code says:
    this.indexMovies();
  },
  methods: {
    moviesIndex: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log("All Movies:", this.movies);
      });
    },
  },
};
</script>
