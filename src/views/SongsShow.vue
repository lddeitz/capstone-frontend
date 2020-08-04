<template>
  <div class="songs-show">
    <div v-if="song.title">
      <div class="song-info">
        <br />
        <div class="row mb-30">
          <div class="col-6">
            <center>
              <div class="container">
                <div class="spacer-2x">&nbsp;</div>
                <h2 class="section-title text-center mb-10">
                  {{ song.title }}
                </h2>
                <div class="spacer-line border-primary">&nbsp;</div>
                <div class="spacer-2x">&nbsp;</div>
              </div>
              <router-link :to="`/songs/${song.id}/edit`">
                <img
                  :src="song.img_url"
                  class="figure-img img-fluid rounded w-50 raised move"
                  alt="album art"
                /><br />
              </router-link>
            </center>
            <div class="spacer-2x">&nbsp;</div>
            <center>
              <router-link
                class="btn btn-primary pill m-1"
                :to="`/songs/${song.id}/edit`"
                >EDIT SONG</router-link
              >
              <!-- <button
                class="btn btn-danger-gradient m-10"
                v-on:click="deleteSong()"
              >
                DELETE SONG
              </button> -->
            </center>
          </div>
        </div>
        <div class="col-6">
          <strong>Details:</strong>

          <p>{{ song.description }}</p>
          <br />
          <strong>Keywords:</strong>
          <p>{{ song.keywords }}</p>
          <br />

          <!--Track Embed-->
          <div class="song-embed">
            <span v-html="song.url"></span>
          </div>
        </div>

        <!--prismic.io-->
        <!-- <div>
        <prismic-embed :field="fields.songEmbed"/>
        </div> -->

        <!--New Comment-->
        <div class="container">
          <h2>New Comment</h2>
          <form v-on:submit.prevent="createComment(song)">
            Notes:<textarea type="text" v-model="newCommentNotes"></textarea
            ><br />
            <small
              >{{ 280 - newCommentNotes.length }} characters remaining.</small
            ><br />
            <div v-if="!$parent.isLoggedIn()">
              Author:<input type="text" v-model="newCommentAuthor" /><br />
            </div>
            Song Timestamp:<input
              type="text"
              v-model="newSongTimestamp"
            /><br />
            <div v-for="tag in tags">
              <input
                :value="tag.id"
                type="checkbox"
                :id="tag.id"
                v-model="tagIds"
              />
              <label :for="tag.id">{{ tag.name }}</label>
            </div>
            {{ tagIds }}
            <input
              type="submit"
              class="btn btn-primary pill m-1"
              value="Comment"
            />
          </form>
        </div>

        <!--All Comments-->
        <div class="total-comments">
          <div v-for="comment in song.comments">
            <strong
              ><p>{{ comment.author }}</p></strong
            >
            <p>{{ comment.notes }}</p>
            <p v-for="tag in comment.tags">{{ tag.name }}</p>
            <p>{{ comment.song_timestamp }}</p>
            <div v-if="$parent.getUserId() == comment.user_id">
              <button v-on:click="showCommentEditForm(comment)">Edit</button>
              <button v-on:click="deleteComment(comment)">Delete</button>
            </div>
            <br />
            <!--Edit Comment Tag Box-->
            <div v-if="comment == currentComment">
              <form v-on:submit.prevent="editComment(currentComment)">
                Notes:<textarea
                  type="textarea"
                  v-model="currentComment.notes"
                ></textarea
                ><br />

                <div v-if="!$parent.isLoggedIn()">
                  Author:<input
                    type="text"
                    v-model="currentComment.author"
                  /><br />
                </div>
                Song Timestamp:<input
                  type="text"
                  v-model="currentComment.song_timestamp"
                /><br />
                <div v-for="tag in tags">
                  <input
                    :value="tag.id"
                    type="checkbox"
                    :id="tag.id"
                    v-model="selectedTagIds"
                  />
                  <label :for="tag.id">{{ tag.name }}</label>
                </div>
                {{ selectedTagIds }}
                <input
                  type="submit"
                  class="btn btn-primary"
                  value="Update Comment"
                />
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      // fields: {
      //   songEmbed: null
      // },
      song: {},
      song_id: "",
      comments: [],
      tagIds: [],
      newCommentNotes: "",
      newCommentAuthor: "",
      newSongTimestamp: "",
      newCommentTags: [],
      artist_name: "",
      errors: [],
      tags: [],
      selectedTagIds: [],
      currentComment: {},
      commentTagFilter: "",
    };
  },
  created: function() {
    // this.getContent(); //prismic.io

    axios.get(`/api/songs/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.song = response.data;
    });

    // axios.get(`/api/songs/${this.$route.params.url}`).then(response => {
    //   console.log(response.data);
    //   this.song.url = response.data;
    // });

    axios.get(`/api/tags/`).then((response) => {
      console.log(response.data);
      this.tags = response.data;
    });
  },
  methods: {
    // getContent: function() {
    //   var params = {
    //     song_url: this.song.url
    //   };
    //   axios.get("/api/songs", params).then(song_url => {
    //     this.fields.songEmbed = song_url.data.songEmbed;
    //   });
    createComment: function() {
      var params = {
        song_id: this.song.id,
        notes: this.newCommentNotes,
        author: this.newCommentAuthor,
        song_timestamp: this.newSongTimestamp,
        tag_ids: this.tagIds,
      };

      axios
        .post("/api/comments", params)
        .then((response) => {
          this.song.comments.push(response.data);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(this.errors);
        });
    },
    showCommentEditForm: function(comment) {
      this.currentComment = comment;
      this.selectedTagIds = this.currentComment.tags.map((tag) => tag.id);
    },

    editComment: function(comment) {
      var params = {
        notes: comment.notes,
        author: comment.author,
        song_timestamp: comment.song_timestamp,
        tag_ids: this.selectedTagIds,
      };

      axios
        .patch(`/api/comments/${comment.id}`, params)
        .then((response) => {
          console.log(response.data);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },

    deleteComment: function(comment) {
      if (confirm("Are you sure you want to delete this comment?")) {
        axios.delete(`/api/comments/${comment.id}`).then((response) => {
          console.log("Comment deleted.", response.data);
          // splice comment out of comment array
        });
      }
    },

    deleteSong: function() {
      if (confirm("Are you sure you want to delete your song?")) {
        axios.delete(`/api/songs/${this.song.id}`).then((response) => {
          console.log("Song deleted.", response.data);
          this.$router.push(`/api/users/${this.user.id}`);
        });
      }
    },
  },
};
</script>

<style></style>
