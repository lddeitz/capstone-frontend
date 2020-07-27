<template>
  <div class="songs-edit">
    <h2>Edit Your Song</h2>
      <div class="edit-form">
        <form v-on:submit="editInfo()">  
          <label for="artist_name">Title:</label>
          <input type="text" v-model="song.title"><br>

          <label for="first_name">Description:</label>
          <input type="text" v-model="song.description"><br>

          <label for="last_name">Keywords:</label>
          <input type="text" v-model="song.keywords"><br>

          <label for="bio">URL:</label>
          <input type="text" v-model="song.url"><br>

          <label for="email">Image:</label>
          <input type="text" v-model="song.img_url"><br>

          <input type="submit" value="Update"><br>
        </form>
      </div>

    <!--Cloudinary Functionality-->
    
    <!-- <div class="edit-img">
      <img :src="song.img_url" alt="img_url"><br>
      <label>Image</label>
      <input type="file" v-on:change="setFile($event)" ref="fileInput">
    </div> -->

    <!-- <div class="delete-song">
      <button v-on:click="deleteSong()">Delete Song</button>
    </div> -->
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
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.image = event.target.files[0];
      }
    },
    editInfo: function() {
      var params = {
        title: this.song.title,
        description: this.song.description,
        keywords: this.song.keywords,
        url: this.song.url,
        image: this.song.url_img
      };
      axios
        .patch(`/api/songs/${this.song.id}`, params)
        .then(response => {
          console.log(response.data);
          this.song = response.data;
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
    // deleteSong: function() {
    //   if (confirm("Are you sure you want to delete your song?")) {
    //     axios.delete(`/api/songs/${this.song.id}`).then(response => {
    //       console.log("Account deleted.", response.data);
    //       this.$router.push("/signup");
    //     });
    //   }
    // }
  }
};
</script>

<style>
</style>