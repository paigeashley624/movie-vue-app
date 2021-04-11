<template>
  <div class="home">
    <div>
      <h1>Add A New Movie</h1>
      Title:
      <input type="text" v-model="newMovieTitle" />
      Year:
      <input type="text" v-model="newMovieYear" />
      Plot:
      <input type="text" v-model="newMoviePlot" />
      Director:
      <input type="text" v-model="newMovieDirector" />
      English:
      <input type="text" v-model="newMovieEnglish" />
      Image:
      <input type="text" v-model="newMovieImage" />
    </div>
    <button v-on:click="createMovie()">Create Movie</button>
    <h1>Best in Theaters Now!!!</h1>
    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <h3>{{ movie.title }}</h3>
        <img v-bind:src="movie.image" v-bind:alt="movie.title" />
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
          <p>
            English:
            <input type="text" v-model="currentMovie.english" />
          </p>
          <button>Close</button>
          <button v-on:click="updateMovie(currentMovie)">Update this Movie</button>
          <button v-on:click="destroyMovie(currentMovie)">Delete this Movie</button>
          <!-- <button>Close</button> -->
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
      newMovieEnglish: "",
      newMovieImage: "",
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
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish,
        image: this.newMovieImage,
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
      console.log(movie);
    },
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
        english: movie.english,
        image: movie.image,
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
