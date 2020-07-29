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

      <!-- New Comment-->
      <h2>New Comment</h2>
      <form v-on:submit.prevent="createComment(song)">
          Tags:<input type="text" v-model="newCommentTags"><br>
          Notes:<input type="text" v-model="newCommentNotes"><br>
          Author:<input type="text" v-model="newCommentAuthor"><br>
          Song Timestamp:<input type="text" v-model="newSongTimestamp"><br>
        <input type="submit" class="btn btn-primary" value="Comment">
      </form>
      </div>

      <!--All Comments-->

      <!-- <div v-if="comments[0].more"> -->
      <div class="total-comments">
        <div v-for="comment in song.comments">
          <strong><p>{{ comment.author }}</p></strong>
          <p>{{ comment.notes }}</p>
          <p>{{ comment.tags }}</p>
          <p>{{ comment.song_timestamp }}</p>
          <br>
        </div>
      </div>
      <!-- </div> -->

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
      // song_id: localStorage.getItem("song_id"),
      song_id: "",
      comments: [],
      tag_ids: [],
      newCommentNotes: "",
      newCommentAuthor: "",
      newSongTimestamp: "",
      newCommentTags: [],
      artist_name: "",
      errors: []
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
    createComment: function(song) {
      // var formData = new FormData();
      // formData.append("notes", this.comment.notes);
      // formData.append("author", this.comment.author);
      // formData.append("song_timestamp", this.comment.song_timestamp);
      // formData.append("tags", this.comment.tags);

      var params = {
        song_id: song.id,
        notes: this.newCommentNotes,
        author: this.newCommentAuthor,
        song_timestamp: this.newSongTimestamp
        // tags: this.newCommentTags
      };

      axios
        .post("/api/comments", params)
        .then(response => {
          // console.log(response.data);
          this.comments.push(response.data);
          // this.comment = response.data;
          // console.log(this.comment);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          console.log(this.errors);
        });
    },

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