<template>
  <div class="songs-new">
    <h2>Submit a Song</h2>

    <form v-on:submit.prevent="createSong()">

        Title: <input type="text" v-model="newSongTitle"><br>

        Description: <input type="text" v-model="newSongDescription"><br>

        Keywords: <input type="text" v-model="newSongKeywords"><br>

        URL: <input type="text" v-model="newSongUrl"><br>

        Artwork: <input type="text" v-model="newSongImgUrl"><br>

        <!-- <label>Artwork:</label>
        <input type="file" v-on:change="setFile($event)" ref="fileInput"> -->

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
      newSongImgUrl: ""
      // user_id: localStorage.getItem("user_id"),
      // song_id: localStorage.getItem("id")
    };
  },
  created: function() {},
  methods: {
    createSong: function() {
      var params = {
        title: this.newSongTitle,
        description: this.newSongDescription,
        keywords: this.newSongKeywords,
        url: this.newSongUrl,
        img_url: this.newSongImgUrl
      };
      axios
        .post("/api/songs", params)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push(`/songs/${response.data.id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
    // setFile: function(event) {
    //   if (event.target.files.length > 0) {
    //     this.imageFile = event.target.files[0];
    //   }
    // }
  }
};
</script>




