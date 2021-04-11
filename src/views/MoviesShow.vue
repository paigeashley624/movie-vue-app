<template>
  <div class="movies-show">
    <div class="container">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <p>{{ movie.director }}</p>
      <p>{{ movie.english }}</p>
      <p>{{ movie.image }}</p>
    </div>
    <div v-if="$parent.getUserId() == movie.user_id">
      <router-link v-bind:to="`/movies/${movie.id}/edit`">See more info</router-link>
      <br />
      <button v-on:click="destroyMovie(movie)">Destroy movie</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    this.showMovies();
  },
  methods: {
    showMovies: function () {
      axios.get("/api/movies/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.movie = response.data;
      });
    },
    destroyMovie: function (movie) {
      axios.delete("/api/movies/" + movie.id).then(() => {
        console.log("You did it! Or whatever!");
        this.$router.push("/movies");
      });
    },
  },
};
</script>
