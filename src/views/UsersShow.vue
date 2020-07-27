<template>
  <div class="users-show">

    <div class="artist-info">
      <h2> {{ user.artist_name }} </h2>
      <img :src="user.profile_picture" alt="profile_picture">
    </div>

    <div class="song-info">
      <h4 v-for="song in user.songs"> Title: {{ song.title }}</h4>
      <!-- <h4 v-for="song in user.songs"> Description: {{ song.img_url }}</h4> -->
      <img v-for="song in user.songs" :src="song.img_url"><br>

      <button v-on:click="editRedirect()" type="button">More Info</button>

      <!-- <div v-if="user === current_user"> -->
        <router-link to="/users/1/edit" tag="button">Edit</router-link>
      <!-- </div> -->
    </div>

    <div class="buttons">
      <!-- <button type="button" v-on:click="">New Song</button>
      <button type="button" v-on:click="">Edit Profile</button> -->
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
    editRedirect() {}
  }
};
</script>

<style>
</style>