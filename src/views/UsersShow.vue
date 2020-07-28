<template>
  <div class="users-show">

    <div class="artist-info">
      <h2> {{ user.artist_name }} </h2>
      <img :src="user.profile_picture" alt="profile_picture">
    </div>

    <div class="song-info">
      <h4 v-for="song in user.songs"> Title: {{ song.title }}</h4>
      <a href="/songs/"><img v-for="song in user.songs" :src="song.img_url"></a><br>

      <button v-on:click="editRedirect()" type="button">More Info</button>

      <!-- <div v-if="user === current_user"> -->
        <!-- <router-link to="/users/1/edit">Edit</router-link> -->
      <button v-on:click="editRedirect()" type="button">Edit Profile</button>
      <button v-on:click="newSongRedirect()" type="button">New Song</button>
      <!-- </div> -->
    </div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      user: {},
      user_id: localStorage.getItem("user_id"),
      songs: []
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.user = response.data;
      console.log(this.user);
    });
  },
  methods: {
    editRedirect() {
      axios.get(`/api/users/${this.$route.params.id}`).then(response => {
        this.$router.push(`/users/${response.data.user_id}/edit`);
      });
    },
    newSongRedirect() {
      axios.get(`/api/songs/${this.$route.params.id}`).then(response => {
        this.$router.push("/songs/new");
      });
    }
  }
};
</script>

<style>
</style>