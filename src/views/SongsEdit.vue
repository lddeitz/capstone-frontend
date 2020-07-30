<template>
  <div class="songs-edit">
    <h2>Edit Your Song</h2>
      <div class="edit-form">
        <form v-on:submit.prevent="editSong()">  

          <!-- <ul>
            <li class="text-danger" v-for="error in errors">{{ error }}</li>
          </ul> -->

          Title:<input type="text" v-model="song.title"><br>

          Description:<input type="text" v-model="song.description"><br>

          Keywords:<input type="text" v-model="song.keywords"><br>

          Embed Link:<input type="text" v-model="song.url"><br>

          Artwork: <input type="file" v-on:change="setFile($event)" ref="fileInput">

          <input type="submit" class="btn btn-primary" value="Update"><br>

        </form>
      </div>

    <!-- <div class="delete-song">
      <button v-on:click="deleteSong()">Delete Song</button>
    </div> -->
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function(song) {
    return {
      errors: [],
      song: {},
      song_id: localStorage.getItem("song_id"),
      title: "",
      description: "",
      keywords: "",
      url: "",
      imageFile: ""
    };
  },
  created: function() {
    axios.get(`/api/songs/${this.$route.params.id}`).then(response => {
      // console.log(response.data);
      // this.song = response.data;
      // console.log(this.song);
      this.song = response.data;
      console.log(this.song);
    });
  },
  methods: {
    editSong: function() {
      var formData = new FormData();
      formData.append("title", this.song.title);
      formData.append("description", this.song.description);
      formData.append("keywords", this.song.keywords);
      formData.append("url", this.song.url);
      formData.append("image_file", this.imageFile);
      axios
        .patch(`/api/songs/${this.song.id}`, formData)
        .then(response => {
          this.$router.push(`/users/${response.data.user_id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.image = event.target.files[0];
      }
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