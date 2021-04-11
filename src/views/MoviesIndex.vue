<template>
  <div class="container movies-index">
    <!-- <div v-for="movie in movies" v-bind:key="movie.id">
      <h3>
        <router-link v-bind:to="`/movies/${movie.id}`">{{ movie.title }}</router-link>
        ({{ movie.year }})
      </h3>
      <p>{{ movie.plot }}</p>
    </div> -->
    Search by name:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <div><button v-on:click="orderBy(movie.title)">Sort Alphabetically</button></div>
    <!-- <div v-for="movie in movies" v-bind:key="movie.id" > -->
    <div
      v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')"
      v-bind:key="movie.id"
      class="card mb-3"
      style="max-width: 540px"
    >
      <div class="row no-gutters">
        <div class="col-md-4">
          <router-link v-bind:to="`/movies/${movie.id}`">
            <img v-bind:src="movie.image" class="card-img" alt="movie.title" />
          </router-link>
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card=text">{{ movie.year }}</p>
            <p class="card-text">
              {{ movie.plot }}
            </p>
            <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  data: function () {
    return {
      movies: [],
      titleFilter: "",
    };
  },
  created() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log("all movies", this.movies);
      });
    },
  },
  mixins: [Vue2Filters.mixin],
};
</script>
