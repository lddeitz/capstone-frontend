<template>
  <div class="songs-show">

    <div class="artist-info">
      <h2> {{ song.title }} </h2><br>
      <img :src="song.img_url" alt="album art"><br>
      <p> {{ song.description }} </p><br>

      <div class="track">
        <p> {{song.url}} </p>
      </div>
      <router-link to="/users/1/edit">Comment</router-link>

    </div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      song: {},
      song_id: localStorage.getItem("song_id")
    };
  },
  created: function() {
    axios.get(`/api/songs/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.song = response.data;
      console.log(this.song);
    });
  },
  methods: {
    editRedirect() {}
  }
};
</script>

<style>
</style>