<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg">
      <a class="navbar-brand col-1" href="/">Blog</a>
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
      <div class="col-2"></div>
      <div class="collapse navbar-collapse justify-content-center" id="navbarNav">
        <ul class="navbar-nav col-8">
          <li class="nav-item active">
            <a class="nav-link" href="/">
              Home
              <span class="sr-only"></span>
            </a>
          </li>
          <li v-if="!isLoggedIn()" class="nav-item">
            <a class="nav-link" href="/signup">Signup</a>
          </li>
          <li v-if="!isLoggedIn()" class="nav-item">
            <a class="nav-link" href="/login">Login</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/posts">Posts</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/posts/new">Create</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/about">About</a>
          </li>
          <li v-if="isLoggedIn()" class="nav-item">
            <a class="nav-link" href="/logout">Logout</a>
          </li>
        </ul>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>

<style>
body {
  font-family: Rockwell Extra Bold, Rockwell Bold, monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  background-image: url("./assets/double-bubble-outline.png");
}

.navbar-brand {
  color: white;
  margin-right: 0rem !important;
}

.navbar {
  background-color: lightcoral;
}

.navbar-nav {
  color: white;
  text-decoration-color: white;
}
</style>
