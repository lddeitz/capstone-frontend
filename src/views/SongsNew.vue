<template>
  <div class="songs-new">
    <!-- <h2>Submit a Song</h2> -->
    <div class="container">
      <div class="spacer-2x">&nbsp;</div>
      <h2 class="section-title text-center mb-10">UPLOAD A TRACK</h2>
      <div class="spacer-line border-primary">&nbsp;</div>
      <div class="spacer-2x">&nbsp;</div>
    </div>
    <!-- / container -->

    <!-- <div class="container">
      <center>
        <form v-on:submit.prevent="createSong()">
          Title: <input type="text" v-model="newSongTitle" /><br />

          Description: <input type="text" v-model="newSongDescription" /><br />

          Keywords: <input type="text" v-model="newSongKeywords" /><br />

          Embed Link: <input type="text" v-model="newSongUrl" /><br />

          Artwork:
          <input
            type="file"
            v-on:change="setFile($event)"
            ref="fileInput"
          /><br />

          <input
            type="submit"
            class="btn btn-primary pill m-1"
            value="Submit"
          />
        </form>
      </center>
    </div> -->

    <div class="container">
      <!-- <div class="row"> -->
        <!-- <div class="col-sm-6"> -->
          <p class="lead mt-3 mb-3"></p>
          <form
            class="validation-inner"
            v-on:submit.prevent="createSong()"
            id="form-validation"
          >
            <div class="form-group">
              Title:
              <input
                type="text"
                class="form-control"
                id="title"
                name="inputTitle"
                placeholder="Feel free to specify a version!"
                v-model="newSongTitle"
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
                placeholder="Any notes on things you're looking for feedback on?"
                v-model="newSongDescription"
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
                placeholder="Give a few words you'd use to describe this track."
                v-model="newSongKeywords"
              />
            </div>
            <!-- / form-group -->
            <div class="form-group">
              Embed URL:
              <textarea
                id="url"
                class="form-control"
                name="embedURL"
                rows="2"
                placeholder="Grab the embedded URL from the source of your choosing."
                v-model="newSongUrl"
                required
              ></textarea>
            </div>
            <!-- / form-group -->
            <div class="row">
              <div class="col-4">
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
              </div>
            </div>
             <div class="spacer-2x">&nbsp;</div>
            <!-- / form-group -->
            <button type="submit" class="btn btn-primary pill m-1">
              Upload
            </button>
          </form>
        <!-- </div> -->
        <!-- / col-sm-6 -->
      <!-- </div> -->
    </div>
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
      imageFile: "",
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
        .then((response) => {
          console.log("Success", response.data);
          this.$router.push(`/songs/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.imageFile = event.target.files[0];
      }
    },
  },
};
</script>
