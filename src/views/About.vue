<template>
  <div class="about">
    <h1>About</h1>
    <h2>
      <ul>
        <li>Need help adding the nav bar and jumbo tron</li>
        <li></li>
      </ul>
    </h2>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [], //storing multiple things here//
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      currentMovie: {}, //storing one thing here//
    };
  },
  methods: {
    createMovie: function () {
      console.log("Creating a movie");
      var params = {
        title: this.newMovieTitle,
        prep_time: this.newMovieYear,
        ingredients: this.newMoviePlot,
        directions: this.newMovieDirector,
      };
      axios
        .post("/api/movies", params)
        .then((response) => {
          console.log(response.data);
          this.movies.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
