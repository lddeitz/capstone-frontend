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
              <!--Button for Modal-->
              <!-- <button
                type="button"
                class="btn btn-primary"
                data-toggle="modal"
                data-target="#commentModal"
              >
                Comment
              </button> -->
              <!--/Button for Modal-->

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
          <div class="col-6">
            <div class="container">
              <div class="spacer-2x">&nbsp;</div>
              <h2 class="section-title text-center mb-10">
                LISTEN
              </h2>
              <div class="spacer-line border-primary">&nbsp;</div>
              <div class="spacer-2x">&nbsp;</div>
            </div>
            <!-- <strong>Description:</strong>

            <p>{{ song.description }}</p>
            <br />
            <strong>Keywords:</strong>
            <p>{{ song.keywords }}</p>
            <br /> -->
            <div class="col-md-10">
              <div class="card">
                <div class="card-body">
                  <div class="promo-left mb-30">
                    <div class="promo-container pl-60">
                      <i
                        class="ti-comment promo-icon fs-40 d-block mb-25 left-30 text-success"
                      ></i>
                      <h6 class="box-title mb-15 text-hover success-hover">
                        DESCRIPTION
                      </h6>
                      <p class="card-text mt-15 mb-0">
                        "{{ song.description }}"
                      </p>
                    </div>
                  </div>
                </div>
              </div>

              <!-- <div class="promo-left mb-30">
                    <div class="promo-container pl-60">
                      <i
                        class="fas fa-star promo-icon fs-40 d-block mb-25 left-30 text-info"
                      ></i>
                      <h6 class="box-title mb-15 text-hover info-hover">
                        KEYWORDS
                      </h6>
                      <p class="card-text mt-15 mb-0">{{ song.keywords }}</p>
                    </div>
                  </div> -->
              <div class="card">
                <div class="card-body">
                  <div class="promo-left">
                    <div class="promo-container pl-60">
                      <i
                        class="ti-world promo-icon fs-40 d-block mb-25 left-30 text-danger"
                      ></i>
                      <h6 class="box-title mb-15 text-hover danger-hover">
                        AUDIO
                      </h6>
                      <!--Track Embed-->
                      <div class="song-embed">
                        <span v-html="song.url"></span>
                      </div>
                    </div>
                  </div>
                </div>
                <!-- / promo-left -->
              </div>
              <!-- / card-body -->
              <!-- </div> -->
              <!-- / card -->
            </div>
            <!-- / column -->
          </div>
        </div>

        <!--prismic.io-->
        <!-- <div>
        <prismic-embed :field="fields.songEmbed"/>
        </div> -->

        <!-- New Comment-->
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

        <!-- <div class="total-comments">
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
            <br /> -->

        <!--Edit Comment Tag Box-->

        <!-- <div v-if="comment == currentComment">
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
        </div> -->
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
