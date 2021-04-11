// what is put on this page applies to every page of the app

<template>
  <div id="app">
    <div id="nav">
      <span>
        <router-link to="/">Home</router-link>
      </span>
      |
      <router-link to="/about">About</router-link>
      |
      <span v-if="isLoggedIn()">
        <router-link to="/logout">Logout</router-link>
      </span>
      <span v-else>
        <router-link to="/signup">Signup</router-link>
        |
        <router-link to="/login">Login</router-link>
      </span>

      |
      <router-link to="/movies">All Movies</router-link>
      |
      <router-link to="/movies/new">Create New Movie</router-link>
      |
    </div>

    <!-- Bootstrap  Navbar  -->

    <!-- <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item active">
            <a class="nav-link" href="/">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li v-if="isLoggedIn()" class="nav-item">
            <a class="nav-link" href="/logout">Logout</a>
          </li>
          <li v-else class="nav-item">
            <a class="nav-link" href="/signup">SignUp</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/login">Login</a>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li>
        </ul>
      </div>
    </nav> -->
    <router-view />
  </div>
</template>

<style>
/* <div class="jumbotron" jumbotron-fluid">
  <div class="container">
    <h1 class="display-4">Fluid jumbotron</h1>
    <p class="lead">This is a modified jumbotron that occupies the entire horizontal space of its parent.</p>
  </div>
</div> */
</style>

<script>
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
