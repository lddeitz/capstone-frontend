<template>
  <div class="home">
    <div style="background-image:url(/assets/images/dj-4595492_1920.jpg)">
      <header class="hero-image">
        <div class="height-90 v-center dark">
          <div class="container">
            <div class="w60 m-auto text-center">
              <h1 class="mb-20">TRACK YOUR MIXING</h1>
              <p class="mb-20">
                You know who your go-to's are when you need mixing advice. Now
                keep their feedback contained in one place as you prep your song
                for the rest of the world.
              </p>
              <a href="/signup" class="btn btn-primary pill">
                <span>CREATE A FREE ACCOUNT</span></a
              >
            </div>
            <!-- / w60 -->
          </div>
          <!-- / container -->
        </div>
        <!-- / height-90 -->
      </header>
    </div>
    <section id="features" class="lg">
      <div class="container">
        <div class="row">
          <div class="col-md-4">
            <div class="promo-box text-center mb-0 dark bg-inverse">
              <i
                class="fas far fa-calendar-alt fs-36 d-block mb-25 text-success"
              ></i>
              <h6 class="box-title mb-15 text-hover success-hover">
                VERSION CONTROL
              </h6>
              <p class="box-description">
                Create a song and collect feedback, updating your song board
                with embedded private links and notes to keep your progress
                organized.
              </p>
            </div>
            <!-- / promo-box -->
          </div>
          <!-- / column -->

          <div class="col-md-4">
            <div class="promo-box text-center mb-0 dark bg-inverse">
              <i
                class="fas fas fa-sliders-h promo-icon fs-36 d-block mb-25 text-primary"
              ></i>
              <h6 class="box-title mb-15 text-hover primary-hover">
                TARGETED FEEDBACK
              </h6>
              <p class="box-description">
                Control who gets to share feedback on your track and keep it as
                hidden as it needs to be until the world is ready for what
                you've created.
              </p>
            </div>
            <!-- / promo-box -->
          </div>
          <!-- / column -->

          <div class="col-md-4">
            <div class="promo-box text-center mb-0 dark bg-inverse">
              <i
                class="fas fa-undo-alt promo-icon fs-36 d-block mb-25 text-warning"
              ></i>
              <h6 class="box-title mb-15 text-hover warning-hover">
                MAKE MORE MUSIC
              </h6>
              <p class="box-description">
                After you've mixed your song to its completion, simply retire
                the song board from your profile and create a new board when you
                need it.
              </p>
            </div>
            <!-- / promo-box -->
          </div>
          <!-- / column -->
        </div>
        <!-- / row -->
      </div>
      <!-- / container -->
    </section>
    <!-- / features -->
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!"
    };
  },
  created: function() {},
  methods: {}
};
</script>
