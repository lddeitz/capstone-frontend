<template>
  <div id="app">
    <body>
        <nav class="navbar navbar-expand-lg dark bg-inverse">
          <div class="container">
            <a class="navbar-brand" href="/">
              <img src="/assets/images/SOUNDJEK-LOGO.png" height="120%" alt=""
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

                <li
                  class="nav-item"
                  v-if="isLoggedIn() && !isEditProfile() && !isHome()"
                >
                  <router-link
                    class="nav-link smooth-scroll"
                    :to="`/users/${getUserId()}/edit`"
                  >
                    EDIT PROFILE</router-link
                  >
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
      <footer class="dark bg-inverse">
        <div class="container text-center">
          <div class="row v-center">
              <p>
                © 2020 <span class="fw-regular">SOUNDJEK</span>. All Rights
                Reserved.
              </p>
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
    isEditProfile: function() {
      return this.$route.name === "users-edit";
    },
    isHome: function() {
      return this.$route.name === "Home";
    },
  },
};
</script>
