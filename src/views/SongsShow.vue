<template>
  <div class="songs-show">

    <div class="song-info">
      <h2> {{ song.title }} </h2><br>
      <img :src="song.img_url" alt="album art"><br>
      <p> {{ song.description }} </p><br>
      <p> {{ song.keywords }} </p><br>

      <!--Track Embed-->
      <div class="song-embed">
        <p> {{song.url}} </p>
      </div>

      <!--New Comment-->
      <div class="new-comment">
        <input type="text">
        <input type="submit" v-on:click="addComment()" value="Add Comment"><br>
      </div>

      <!--All Comments-->
      <div class="total-comments">
        <p v-for="comment in song.comments"> {{ comment.author }} </p>
        <p v-for="comment in song.comments"> {{ comment.notes }} </p>
        <p v-for="comment in song.comments"> {{ comment.song_timestamp }} </p>
      </div>

      <!--Song Delete (for uploader only)-->
      <div class="delete-song">
        <button v-on:click="deleteSong()">Delete Song</button>
      </div>

    </div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      song: {},
      song_id: localStorage.getItem("song_id"),
      comments: []
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
    addComment() {},

    deleteSong: function() {
      if (confirm("Are you sure you want to delete your song?")) {
        axios.delete(`/api/songs/${this.song.id}`).then(response => {
          console.log("Song deleted.", response.data);
          this.$router.push(`/api/users/${this.user.id}`);
        });
      }
    }
  }
};
</script>

<style>
</style>