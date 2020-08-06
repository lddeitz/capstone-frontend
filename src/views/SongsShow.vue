<template>
  <div class="songs-show">
  <div class="container">
    <div class="spacer-2x">&nbsp;</div>
    <h2 class="section-title text-center mb-10">MIXING FEEDBACK<br></h2>
    <div class="spacer-line border-primary">&nbsp;</div>
    <div class="spacer-2x">&nbsp;</div>
  </div>
      <section class="big bg-white">
          <div class="container">
              <div class="row v-center">
                  <div class="col-md-6">
                      <h4 class="mb-20">{{song.title}}</h4>
                      <strong><p class="fw-regular fs-12 text-black mb-2">
                      KEYWORDS: {{ song.keywords }}</p></strong
                      <p class="mb-30 lead">"{{song.description}}"</p>
                      <div class="spacer-2x">&nbsp;</div>
                    <center>
                      <div class="promo-box p-y-10 bg-transparent">
                          <div class="promo-container-big">
                            <span v-html="song.url"></span>
                          </div><!-- / promo-container -->
                         
                      
                      </div><!-- / promo-box -->
                      </center>

                      <div class="promo-box pt-10 pb-0 mb-0 tablet-top-45 promo-center bg-transparent">
                          <div class="promo-container-big">
                            <img
                        :src="song.img_url"
                        alt=""
                        class="promo-box-image rounded img-md mb-25">
                        <br>
                              <router-link
                              class="btn btn-primary pill m-1 success"
                              :to="`/songs/${song.id}/edit`"
                              >EDIT SONG</router-link>
                          </div><!-- / promo-container -->
                      </div><!-- / promo-box -->
                  </div><!-- / column -->

                  <div class="col-md-6">
                      <div class="form-holder p-y-40 p-x-30 rounded bg-white raised">
                          <form v-on:submit.prevent="createComment(song)" class="validation-inner" id="commentForm">
                              <div class="row">
                                <div class="form-group col-6">
                                  TIMESTAMP: <input id="song_timestamp" v-model="newSongTimestamp" class="form-control border-faded" placeholder="0:00 - 0:02">
                              </div>
                                  <div class="col-md-12 sub-col-left">
                                      NOTES:<div class="form-group">
                                        <textarea type="text" v-model="newCommentNotes" class="form-control border-faded" id="notes" 
                                        required placeholder="Drop a note if something sounds like it could be improved!"></textarea>
                                      </div>
                                      <span v-if="newCommentNotes.length > 0">
                                        <small>{{ 280 - newCommentNotes.length }} characters remaining</small>
                                      </span><!-- / form-group -->
                                  </div><!-- / column -->
                                  <div class="col-md-6 sub-col-right">
                                      <div class="form-group" v-if="!$parent.isLoggedIn()">
                                          NAME: <input v-model="newCommentAuthor" type="text" class="form-control border-faded" id="author" placeholder="Author" required>
                                      </div><!-- / form-group -->
                                  </div><!-- / column -->
                              </div><!-- / row -->
                              <div class="form-group">
                                TAGS:
                                <div class="col-md-12">
                                   <div class="checkbox" v-for="tag in tags">
                                    <br>
                                    <label class="hidden"><input type="list checkbox"></label>
                                    <input  type="checkbox" :value="tag.id"
                                    :id="tag.id"
                                    v-model="tagIds">
                                    <label :for="tag.id"><span class="fw-light">{{ tag.name }}</span></label><br>
                                </div>
                              </div><!-- / form-group -->
                            </div>
                            
                            <center>
                              <button type="submit" class="btn btn-md btn-primary btn-submit rounded col-6">COMMENT</button> 
                              </center>
                          </form><!-- / contact-form -->
                      </div><!-- / form-holder -->
                  </div><!-- / column -->
              </div><!-- / row -->
          </div><!-- / container -->
      </section><!-- / contact -->

      <div v-for="comment in song.comments">
        <div class="card card-rounded col-12  ">
          <div class="card-body">
            <strong
          ><h6>{{ comment.author }}</h6></strong
        >
        <p>{{ comment.notes }}</p>
              <div class="tag-cloud">
                  <p v-for="tag in comment.tags" class="badge badge-primary badge-pill">#{{ tag.name }}</p>
              </div><!-- / tag-cloud -->
          <!-- <p v-for="tag in comment.tags">{{ tag.name }}</p> -->
        <p>{{ comment.song_timestamp }}</p>

        <div v-if="$parent.getUserId() == comment.user_id">

          <button class="btn btn-secondary m-1" v-on:click="showCommentEditForm(comment)">Edit</button>
          <button class="btn btn-secondary m-1" v-on:click="deleteComment(comment)">Delete</button>
        </div>
        <br />

        <div v-if="comment == currentComment">
          <form v-on:submit.prevent="editComment(currentComment)">
            Notes:<br><textarea
              type="textarea col-6"
              v-model="currentComment.notes"
            ></textarea
            ><br />
            <div class="spacer-2x">&nbsp;</div>

            <div v-if="!$parent.isLoggedIn()">
              Author:<br><input
                type="text"
                v-model="currentComment.author"
              /><br />
            </div>
            <div class="spacer-2x">&nbsp;</div>
            Song Timestamp:<br><input
              type="text"
              class="col-2"
              v-model="currentComment.song_timestamp"
            /><br />
            <div class="spacer-2x">&nbsp;</div>
            Tags:
            <div v-for="tag in tags">
              <input
                :value="tag.id"
                type="checkbox"
                class="card-body"
                :id="tag.id"
                v-model="selectedTagIds"
              />
              <label :for="tag.id">{{ tag.name }}</label>
            </div>
            <input
              type="submit"
              class="btn btn-primary"
              value="Update Comment"
            />
          </form>
        </div>
      </div>
          </div>
        </div><!-- / card -->
      <!-- <ul class="media-list">
          <li class="media">
            <div v-for="comment in song.comments">
              <div class="media-body">
                  <div class="comment-info">
                      <div class="comment-author">{{ comment.author }}</div>
                      <p v-for="tag in comment.tags">{{ tag.name }}</p>
                      <p>{{ comment.song_timestamp }}</p>
                  </div>
                  <div class="comment">
                      <p class="mb-0">{{ comment.notes }}</p>
                  </div>
              </div>
            </div>
          </li>
      </ul> -->
      <div class="spacer-2x">&nbsp;</div>
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

    // axios.get(`/api/users/`).then(response => {
    //   console.log(response.data);
    //   this.users = response.data;
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
          // comment.splice(0,1);
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
