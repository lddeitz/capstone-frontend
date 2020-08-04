<template>
  <div id="app">
    <head>
      <!-- Meta -->
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta
        name="viewport"
        content="width=device-width, initial-scale=1, shrink-to-fit=no"
      />
      <meta name="description" content="ERIKA - Bootstrap 4 UI & Components" />
      <meta name="author" content="erikathemes.com" />
      <!-- Favicon -->
      <link rel="icon" href="assets/images/favicon.png" />
      <!-- Site Title -->
      <title>ERIKA - Bootstrap 4 UI & Components</title>
      <!-- Bootstrap 4 core CSS -->
      <link href="assets/css/bootstrap.min.css" rel="stylesheet" />
      <!-- Custom Styles -->
      <link href="assets/css/style.css" rel="stylesheet" />
      <link href="assets/css/animate.css" rel="stylesheet" />
      <link href="assets/css/owl.carousel.min.css" rel="stylesheet" />
      <!-- Fonts -->
      <link
        href="https://fonts.googleapis.com/css?family=Montserrat:300,400,700"
        rel="stylesheet"
      />
      <link
        href="https://fonts.googleapis.com/icon?family=Material+Icons"
        rel="stylesheet"
      />
      <link
        href="assets/css/fontawesome-all.min.css"
        rel="stylesheet"
        type="text/css"
      />
      <link rel="stylesheet" href="assets/css/themify-icons.css" />
    </head>

    <body>
      <header
        class="bg-white pt-10 bg-img bg-fixed"
        style="background-image: url(assets/images/erika-header.jpg)"
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
                <div v-if="isLoggedIn()">
                  <div v-if="!isProfile()">
                    <li class="nav-item">
                      <router-link
                        class="nav-link smooth-scroll"
                        :to="`/users/${getUserId()}/`"
                        >MY PROFILE</router-link
                      >
                    </li>
                  </div>

                  <li class="nav-item">
                    <router-link class="nav-link smooth-scroll" to="/songs/new">
                      <div v-if="!isNewSong()">
                        NEW SONG
                      </div>
                    </router-link>
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
    </body>
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
