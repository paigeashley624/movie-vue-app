<template>
  <div class="home">
    <div>
      <h1>New movie</h1>
      Title:
      <input type="text" v-model="newMovieTitle" />
      Year:
      <input type="text" v-model="newMovieYear" />
      Plot:
      <input type="text" v-model="newMoviePlot" />
      Director:
      <input type="text" v-model="newMovieDirector" />
    </div>
    <button v-on:click="createMovie()">Create Movie</button>
    <h1>All Movies</h1>
    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <h3>{{ movie.title }}</h3>
        <img v-bind:src="movie.image_url" v-bind:alt="movie.title" />
        <p>{{ movie.user }}</p>
        <button v-on:click="showMovie(movie)">More Info!</button>
      </div>
      <dialog id="movie-details">
        <form method="dialog">
          <h1>movie Info</h1>
          <p>
            Title:
            <input type="text" v-model="currentMovie.title" />
          </p>
          <p>
            PrepTime:
            <input type="text" v-model="currentMovie.prep_time" />
          </p>
          <p>
            Ingredients:
            <input type="text" v-model="currentMovie.ingredients" />
          </p>
          <p>
            Directions:
            <input type="text" v-model="currentMovie.directions" />
          </p>
          <p>
            ImageUrl:
            <input type="text" v-model="currentMovie.image_url" />
          </p>
          <button v-on:click="updatemovie(currentMovie)">Update</button>
          <button v-on:click="destroymovie(currentMovie)">Destroy</button>
          <button>Close</button>
        </form>
      </dialog>
    </div>
  </div>
</template>
<style></style>

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
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log("all movies:", this.movies);
      });
    },
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
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        prep_time: movie.prep_time,
        ingredients: movie.ingredients,
        directions: movie.directions,
        image_url: movie.image_url,
      };
      axios.patch("/api/movies/" + movie.id, params).then((response) => {
        console.log("Success", response.data);
      });
    },
    destroyMovie: function (movie) {
      axios.delete("/api/movies/" + movie.id).then((response) => {
        console.log("Success!", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>
