<template>
  <div class="users-show">
    <div class="artist-info">
      <h2>{{ user.artist_name }}</h2>

      <img
        v-if="user.profile_picture"
        :src="user.profile_picture"
        :alt="user.name"
        class="ppic"
        width="200"
        height="200"
      />
      <img
        v-if="!user.profile_picture"
        :src="'../default-photo.png'"
        :alt="user.name"
        class="ppic"
        width="200"
        height="200"
      />
    </div>

    <div class="song-info">
      <div v-for="song in user.songs">
        <h3>{{ song.title }}</h3>
        <router-link :to="`/songs/${song.id}/`"
          ><img :src="song.img_url"/><br
        /></router-link>
        <router-link :to="`/songs/${song.id}/edit`">Edit Song</router-link>
      </div>
      <router-link :to="`/users/${user.id}/edit`">Edit Profile</router-link>
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
