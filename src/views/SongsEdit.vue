<template>
  <div class="songs-edit">
    <!-- <h2>Edit Your Song</h2> -->
    <div class="container">
      <div class="spacer-2x">&nbsp;</div>
      <h2 class="section-title text-center mb-10">EDIT SONG</h2>
      <div class="spacer-line border-primary">&nbsp;</div>
      <div class="spacer-2x">&nbsp;</div>
    </div>
    <!-- / container -->

    <div class="edit-form">
      <!-- <div class="container">
        <form v-on:submit.prevent="editSong()">
          <ul>
              <li class="text-danger" v-for="error in errors">{{ error }}</li>
            </ul>

          Title:<input type="text" v-model="song.title" /><br />

          Description:<input type="text" v-model="song.description" /><br />

          Keywords:<input type="text" v-model="song.keywords" /><br />

          Embed Link:<input type="text" v-model="song.url" /><br />

          Artwork:
          <input type="file" v-on:change="setFile($event)" ref="fileInput" />

          <input type="submit" class="btn btn-primary" value="Update" /><br />
        </form>
      </div> -->

      <div class="container">
        <!-- <div class="row mb-30"> -->
          <!-- <div class="col-sm-6"> -->
            <p class="lead mt-3 mb-3"></p>
            <form
              class="validation-inner"
              v-on:submit.prevent="editSong()"
              id="form-validation"
            >
              <div class="form-group">
                Title:
                <input
                  type="text"
                  class="form-control"
                  id="title"
                  name="inputTitle"
                  placeholder="Title"
                  v-model="song.title"
                  required
                />
              </div>
              <!-- / form-group -->
              <div class="form-group">
                Description:
                <textarea
                  type="text"
                  class="form-control"
                  id="description"
                  rows="5"
                  name="inputDescription"
                  placeholder="Description"
                  v-model="song.description"
                  required
                /></textarea>
              </div>
              <!-- / form-group -->
              <div class="form-group">
                Keywords:
                <input
                  type="text"
                  class="form-control"
                  id="keywords"
                  name="inputKeywords"
                  placeholder="Keywords"
                  v-model="song.keywords"
                />
              </div>
              <!-- / form-group -->
              <div class="form-group">
                Embed URL:
                <textarea
                  id="url"
                  class="form-control"
                  name="embedURL"
                  rows="1"
                  placeholder="Embed URL"
                  v-model="song.url"
                  required
                ></textarea>
              </div>
              <!-- / form-group -->
              <!-- <div class="row mb-30"> -->
                <!-- <div class="col-6"> -->
                    <div class="form-group">
                      Artwork:
                      <input
                        type="file"
                        id="artwork"
                        name="inputArtwork"
                        placeholder="Artwork"
                        v-on:change="setFile($event)"
                        ref="fileInput"
                      />
                    </div>
                <!-- </div> -->
              <!-- </div> -->
              <!-- / form-group -->
              <button type="submit" class="btn btn-primary pill m-1">
                UPDATE SONG
              </button>
            </form>
          <!-- </div> -->
          <!-- / col-sm-6 -->
        <!-- </div> -->
      </div>
      <div class="spacer">&nbsp;</div>
      <div class="spacer">&nbsp;</div>

      <center>
        <div class="delete-song">
          <button
            class="btn btn-danger-gradient m-10"
            v-on:click="deleteSong()"
          >
            DELETE SONG
          </button>
        </div>
      </center>
    </div>
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
      // imageFile: ""
    };
  },
  created: function() {
    axios.get(`/api/songs/${this.$route.params.id}`).then((response) => {
      // console.log(response.data);
      // this.song = response.data;
      // console.log(this.song);
      this.song = response.data;
      console.log(this.song);
    });
  },
  methods: {
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.song.img_url = event.target.files[0];
      }
    },
    editSong: function() {
      var formData = new FormData();

      formData.append("title", this.song.title);
      formData.append("description", this.song.description);
      formData.append("keywords", this.song.keywords);
      formData.append("url", this.song.url);
      // formData.append("image_file", this.imageFile);
      if (this.song.img_url) {
        formData.append("img_url", this.song.img_url);
      }
      axios
        .patch(`/api/songs/${this.song.id}`, formData)
        .then((response) => {
          this.$router.push(`/songs/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    deleteSong: function() {
      if (confirm("Are you sure you want to delete your song?")) {
        axios.delete(`/api/songs/${this.song.id}`).then(response => {
          console.log("Song deleted.", response.data);
          this.$router.push(`/users/${response.data.user_id}`);
        });
      }
    }
  },
};
</script>

<style></style>
