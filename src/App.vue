<template>
  <div id="app">
    <header class="bg-white pt-10 bg-img bg-fixed">
      <nav class="navbar navbar-expand-lg navbar-light">
        <div class="container">
          <a class="navbar-brand" href="/index.html">
            <img src="/assets/images/logo.png" alt=""
          /></a>

          <button
            class="navbar-toggler collapsed"
            type="button"
            data-toggle="collapse"
            data-target="#navbar-toggle"
            aria-controls="navbar-toggle"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="icon-bar top-bar"></span>
            <span class="icon-bar middle-bar"></span>
            <span class="icon-bar bottom-bar"></span>
            <span class="sr-only">Toggle navigation</span></button
          ><!-- / navbar-toggler -->

          <!--nav start-->
          <div class="collapse navbar-collapse" id="navbar-toggle">
            <ul class="navbar-nav ml-auto">
              <div v-if="isLoggedIn()">
                <li class="nav-item">
                  <router-link
                    class="nav-link smooth-scroll"
                    :to="`/users/${getUserId()}/`"
                    >MY PROFILE</router-link
                  >
                </li>

                <li class="nav-item">
                  <router-link class="nav-link smooth-scroll" to="/songs/new"
                    >NEW SONG</router-link
                  >
                </li>

                <li class="nav-item">
                  <router-link class="nav-link smooth-scroll" to="/logout"
                    >LOGOUT</router-link
                  >
                </li>
              </div>

              <div v-if="!isLoggedIn()">
                <li class="nav-item">
                  <router-link class="nav-link smooth-scroll" to="/signup"
                    >SIGNUP</router-link
                  >
                </li>
                <li class="nav-item">
                  <router-link class="nav-link smooth-scroll" to="/login"
                    >LOGIN</router-link
                  >
                </li>
              </div>
            </ul>
          </div>
          <!--nav end-->

          <!-- / navbar-collapse -->
        </div>
        <!-- / container -->
      </nav>
    </header>

    <router-view />
    <!--Start of Footer-->
    <!--End of Footer-->
  </div>
</template>

<script>
export default {
  data: function() {
    return {};
  },
  methods: {
    // returns true or false depending on jwt in localstorage
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
    getUserId: function() {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
