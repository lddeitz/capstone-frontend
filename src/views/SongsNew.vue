<template>
  <div class="songs-new">
    <h2>Submit a Song</h2>

    <form v-on:submit.prevent="createSong()">

        Title: <input type="text" v-model="newSongTitle"><br>

        Description: <input type="text" v-model="newSongDescription"><br>

        Keywords: <input type="text" v-model="newSongKeywords"><br>

        Embed Link: <input type="text" v-model="newSongUrl"><br>

        Artwork: <input type="file" v-on:change="setFile($event)" ref="fileInput">

    <input type="submit" class="btn btn-primary" value="Submit">

    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      song: {},
      user: {},
      newSongTitle: "",
      newSongDescription: "",
      newSongKeywords: "",
      newSongUrl: "",
      // newSongImgUrl: "",
      imageFile: ""
      // user_id: localStorage.getItem("user_id"),
      // song_id: localStorage.getItem("id")
    };
  },
  created: function() {},
  methods: {
    createSong: function() {
      var formData = new FormData();
      formData.append("title", this.newSongTitle);
      formData.append("description", this.newSongDescription);
      formData.append("keywords", this.newSongKeywords);
      formData.append("url", this.newSongUrl);
      formData.append("image_file", this.imageFile);
      axios
        .post("/api/songs", formData)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push(`/songs/${response.data.id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.imageFile = event.target.files[0];
      }
    }
  }
};
</script>




