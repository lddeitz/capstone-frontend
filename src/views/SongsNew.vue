<template>
  <div class="songs-new">
    <h2>Submit a Song, {{ song.user.artist_name }} </h2>

    <form v-on:submit="newSong()">

        <label for="title">Title:</label>
        <input type="text" v-model="song.title"><br>

        <label for="description">Description:</label>
        <input type="text" v-model="song.description"><br>

        <label for="keywords">Keywords:</label>
        <input type="text" v-model="song.keywords"><br>

        <label for="url">URL:</label>
        <input type="text" v-model="song.url"><br>

        <!-- <label for="img_url">Artwork:</label>
        <input type="text" v-model="song.img_url"><br> -->

        <label>Artwork:</label>
        <input type="file" v-on:change="setFile($event)" ref="fileInput">

        <input type="submit" value="Create"><br>

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
      title: "",
      description: "",
      keywords: "",
      url: "",
      img_url: "",
      user_id: localStorage.getItem("user_id")
    };
  },
  created: function() {},
  methods: {
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.imageFile = event.target.files[0];
      }
    }
  },
  newSong: function() {
    var formData = new formData();
    formData.append("title", this.song.title);
    formData.append("description", this.song.description);
    formData.append("keywords", this.song.keywords);
    formData.append("url", this.song.url);
    formData.append("img_url", this.song.img_url);
    axios
      .post("/api/songs", formData)
      .then(response => {
        this.$router.push(`/songs/${response.data.id}`);
      })
      .catch(error => {
        this.errors = error.response.data.errors;
      });
  }
};
</script>