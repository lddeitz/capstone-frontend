<template>
  <div class="songs-show">

    <div class="song-info">
      <h2> {{ song.title }} </h2><br>
      <img :src="song.img_url" alt="album art"><br>
      <strong>Details:</strong> <p> {{ song.description }} </p><br>
      Keywords:<p> {{ song.keywords }} </p><br>

      <!--Track Embed-->
      <div class="song-embed">
        {{song.url}} 
      </div>

      <!-- New Comment-->
      <h2>New Comment</h2>
      <form v-on:submit.prevent="createComment()">
          Notes:<input type="text" v-model="newCommentNotes"><br>
          <div v-if="!$parent.isLoggedIn()">
            Author:<input type="text" v-model="newCommentAuthor"><br>
          </div>
          Song Timestamp:<input type="text" v-model="newSongTimestamp"><br>
          <div v-for="tag in tags">
            <input :value="tag.id" type="checkbox" :id="tag.id" v-model="tagIds">
            <label :for="tag.id">{{ tag.name }}</label>
          </div>
          {{ tagIds }}
        <input type="submit" class="btn btn-primary" value="Comment">
      </form>

      <!--All Comments-->

      <div class="total-comments">
        <div v-for="comment in song.comments">
          <strong><p>{{ comment.author }}</p></strong>
          <p>{{ comment.notes }}</p>
          <p>{{ comment.tags }}</p>
          <p>{{ comment.song_timestamp }}</p>
          <button v-on:click="editComment(comment)">Edit</button>
          <button v-on:click="deleteComment(comment)">Delete</button>
          <br>
        </div>
      </div>


      <!--Song Delete (for uploader only)-->
      <div class="delete-song">
        <router-link :to="`/songs/${song.id}/edit`">Edit Song</router-link>
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
      newCommentNotes: "",
      newCommentAuthor: "",
      newSongTimestamp: "",
      tagIds: [],
      errors: [],
      tags: []
    };
  },
  created: function() {
    axios.get(`/api/songs/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.song = response.data;
    });
    axios.get(`/api/tags/`).then(response => {
      console.log(response.data);
      this.tags = response.data;
    });
  },
  methods: {
    createComment: function() {
      var params = {
        song_id: this.song.id,
        notes: this.newCommentNotes,
        author: this.newCommentAuthor,
        song_timestamp: this.newSongTimestamp,
        tag_ids: this.tagIds
      };

      axios
        .post("/api/comments", params)
        .then(response => {
          this.song.comments.push(response.data);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          console.log(this.errors);
        });
    },

    editComment: function(comment) {
      var params = {
        notes: comment.notes,
        author: comment.author,
        song_timestamp: comment.song_timestamp,
        tags: comment.tags
      };

      axios
        .patch(`/api/comments/${this.comment.id}`, params)
        .then(response => {
          this.$router.push(`/songs/${response.data.id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },

    deleteComment: function(comment) {
      if (confirm("Are you sure you want to delete this comment?")) {
        axios.delete(`/api/comments/${comment.id}`).then(response => {
          console.log("Comment deleted.", response.data);
          // splice comment out of comment array
        });
      }
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