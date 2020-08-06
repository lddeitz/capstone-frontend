<template>
  <div class="users-show">
    <body>
      <div class="container">
        <div class="spacer-2x">&nbsp;</div>
        <h2 class="section-title text-center mb-10">SONG BOARD</h2>
        <div class="spacer-line border-primary">&nbsp;</div>
        <div class="spacer-2x">&nbsp;</div>
        <center>
          <p>
            To navigate into one of the song's feedback views, click on the
            artwork.
          </p>
        </center>
        <div class="spacer-2x">&nbsp;</div>
      </div>
      <!-- <div class="artist-info">
        <h2>{{ user.artist_name }}</h2>

        <div class="col-md-4">
          <div class="">
            <div class="card-body text-center">
              <img
                class="mb-30 circle"
                style="max-width:65%;"
                v-if="user.profile_picture"
                :src="user.profile_picture"
                :alt="user.artist_name"
              />
              <h6 class="card-title mb-10">{{ user.artist_name }}</h6>
              <p class="mb-0 fs-15 fw-regular">
                {{ user.first_name }} {{ user.last_name }}
              </p>
              <p class="card-text mb-30">{{ user.bio }}</p>
              <p class="mb-0">
                <router-link
                  class="btn btn-primary pill m-1"
                  :to="`/users/${user.id}/edit`"
                  >Edit Profile</router-link
                >
              </p>
            </div>
          </div>
        </div>
      </div>

      <div v-for="song in user.songs">
        <div class="col-md-3">
          <router-link :to="`/songs/${song.id}/`">
            <center>
              <p class="lead mt-3 mb-3">{{ song.title }}</p>
            </center>
            <center>
              <img
                :src="song.img_url"
                class="figure-img img-fluid rounded w-75 raised move"
                :alt="`${song.title}`"
              />
            </center>
          </router-link>
          <center>
            <router-link class="btn btn-success m-1" :to="`/songs/${song.id}/`"
              >VIEW</router-link
            >
          </center>
        </div>

        <router-link
          class="btn btn-primary pill m-1"
          :to="`/songs/${song.id}/edit`"
          >Edit Song</router-link
        >
      </div> -->
      <section id="shop" class="lg bg-white pb-70">
        <div class="container">
          <div class="section-heading text-center">
            <div class="widget text-center p-y-10">
              <!-- <router-link :to="`/users/${user.id}/edit`">
                <img
                  v-if="user.profile_picture"
                  :src="user.profile_picture"
                  :alt="user.artist_name"
                  class="circle w20 mb-15"
                />
              </router-link>
              <h2 class="mb-15">{{ user.artist_name }}</h2>
              <p class="mb-0 fs-15 fw-regular">
                {{ user.first_name }} {{ user.last_name }}
              </p>
              <p class="w50 mb-70 m-x-auto">
                {{ user.bio }}
              </p> -->
            </div>
          </div>
          <!-- / section-heading -->
          <h2></h2>
          <div class="row">
            <div class="col-sm-6 col-md-3 mb-30">
              <div v-for="song in user.songs">
                <div class="product text-center">
                  <!-- / sale-badge -->
                  <div class="container">
                    <router-link :to="`/songs/${song.id}/`">
                      <img
                        :src="song.img_url"
                        alt=""
                        class="mb-30 rounded raised"
                      />
                    </router-link>
                  </div>
                  <p class="mb-1">
                    <a
                      :href="`/songs/${song.id}/`"
                      class="card-title fs-18 fw-regular title-link"
                      >{{ song.title }}</a
                    >
                  </p>
                  <!-- <router-link
                    class="btn btn-success m-1"
                    :to="`/songs/${song.id}/`"
                    >VIEW</router-link
                  > -->
                  <router-link
                    class="btn btn-primary pill m-2"
                    :to="`/songs/${song.id}/edit`"
                    >Edit Song</router-link
                  >
                  <div class="spacer-2x">&nbsp;</div>
                </div>
                <!-- / product -->
              </div>
            </div>
            <!-- / column -->
          </div>
          <!-- / row -->
        </div>
        <!-- / container -->
      </section>
      <!-- / shop -->
    </body>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      user: {},
      songs: [],
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
      console.log(this.user);
    });
  },
  methods: {
    editRedirect() {
      axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
        this.$router.push(`/users/${response.data.user_id}/edit`);
      });
    },
    newSongRedirect() {
      axios.post("/api/songs/").then((response) => {
        this.$router.push("/songs/new");
      });
    },
    editSongRedirect() {
      axios.get(`/api/songs/${this.$route.params.id}`).then((response) => {
        this.$router.push(`/songs/${this.$route.params.id}/edit`);
      });
    },
  },
};
</script>
