<template>
  <div id="app">
    <body>
      <header
        class="bg-white pt-10 bg-img bg-fixed"
        style="background-image: url(/assets/images/erika-header.jpg)"
      >
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
                <li class="nav-item" v-if="isLoggedIn() && !isProfile()">
                  <router-link
                    class="nav-link smooth-scroll"
                    :to="`/users/${getUserId()}/`"
                    >MY PROFILE</router-link
                  >
                </li>

                <li class="nav-item" v-if="!isNewSong() && isLoggedIn()">
                  <router-link class="nav-link smooth-scroll" to="/songs/new">
                    NEW SONG
                  </router-link>
                </li>

                <li class="nav-item" v-if="isLoggedIn()">
                  <router-link class="nav-link smooth-scroll" to="/logout"
                    >LOGOUT</router-link
                  >
                </li>

                <li class="nav-item" v-if="!isLoggedIn()">
                  <router-link class="nav-link smooth-scroll" to="/signup"
                    >SIGNUP</router-link
                  >
                </li>
                <li class="nav-item" v-if="!isLoggedIn()">
                  <router-link class="nav-link smooth-scroll" to="/login"
                    >LOGIN</router-link
                  >
                </li>
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
      <div class="spacer-2x">&nbsp;</div>
      <footer class="dark bg-inverse">
        <div class="container text-center">
          <div class="row v-center">
            <div class="col-lg-6 footer-left-area">
              <p>
                © 2020 <span class="fw-regular">SOUNDJEK</span>. All Rights
                Reserved.
              </p>
            </div>
            <!-- / footer-left-area
          <div class="col-lg-6 footer-right-area">
            <p>
              Designed with
              <span class="fa fa-heart text-danger text-xs va-middle"></span> by
              <a
                href="https://erikathemes.com"
                class="footer-link"
                target="_blank"
                ></a
              >
            </p>
          </div>
          <!-- / footer-right-area -->
          </div>
          <!-- / row -->
        </div>
        <!-- / container -->
      </footer>
      <!--End of Footer-->
    </body>
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
    isProfile: function() {
      return this.$route.name === "users-show";
    },
    isNewSong: function() {
      return this.$route.name === "songs-new";
    },
  },
};
</script>
