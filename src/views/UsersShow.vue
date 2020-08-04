<template>
  <div class="users-show">
    <div class="artist-info">
      <!-- <h2>{{ user.artist_name }}</h2> -->

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
              <!-- <a
                href="#x"
                class="btn btn-sm btn-facebook btn-circle btn-icon m-1"
                ><i class="fab fa-facebook-f"></i
              ></a>
              <a
                href="#x"
                class="btn btn-sm btn-twitter btn-circle btn-icon m-1"
                ><i class="fab fa-twitter"></i
              ></a>
              <a
                href="#x"
                class="btn btn-sm btn-dribbble btn-circle btn-icon m-1"
                ><i class="fab fa-dribbble"></i
              ></a> -->
            </p>
          </div>
          <!-- / card-body -->
        </div>
        <!-- / card -->
      </div>
      <!-- / column -->

      <!-- <img class="mb-30 circle" style="max-width:65%;"
        v-if="user.profile_picture"
        :src="user.profile_picture"
        :alt="user.name"
      /> -->
      <!-- <img
        v-if="!user.profile_picture"
        :src="'../default-photo.png'"
        :alt="user.name"
        width="200"
        height="200"
      /> -->
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
          <!-- <button class="btn btn-primary pill m-1">Open Song</button> -->
          <router-link class="btn btn-success m-1" :to="`/songs/${song.id}/`"
            >VIEW</router-link
          >
        </center>
      </div>

      <!-- <router-link
        class="btn btn-primary pill m-1"
        :to="`/songs/${song.id}/edit`"
        >Edit Song</router-link
      > -->
    </div>
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

<style></style>
