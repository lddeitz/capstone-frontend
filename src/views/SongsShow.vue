<template>
  <div class="songs-show">
    <!-- <div v-if="song.title">
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
              <button
                class="btn btn-danger-gradient m-10"
                v-on:click="deleteSong()"
              >
                DELETE SONG
              </button>
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

              <div class="promo-left mb-30">
                <div class="promo-container pl-60">
                  <i
                    class="fas fa-star promo-icon fs-40 d-block mb-25 left-30 text-info"
                  ></i>
                  <h6 class="box-title mb-15 text-hover info-hover">
                    KEYWORDS
                  </h6>
                  <p class="card-text mt-15 mb-0">{{ song.keywords }}</p>
                </div>
              </div>
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
                      <div class="song-embed">
                        <span v-html="song.url"></span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

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
    </div> -->
    <section id="about">
      <div class="container">
        <div class="box-w-image promo-box bg-transparent pl-45 pr-45">
          <div class="row">
            <div class="col-md-5 bg-img box-bg-image tablet-top-30">
              <center>
                <img
                  :src="song.img_url"
                  class="figure-img img-fluid rounded w-75 raised move"
                  alt="album art"
                />
                <div class="spacer-2x">&nbsp;</div>
                <router-link
                  class="btn btn-primary pill m-1"
                  :to="`/songs/${song.id}/edit`"
                  >EDIT SONG</router-link
                >
              </center>
              <p class="mb-0"></p>
            </div>
            <div class="col-md-7 col-md-offset-5">
              <div class="box-description pl-15">
                <h6 class="mb-15">{{ song.title }}</h6>
                <strong
                  ><p class="fw-regular fs-12 text-black mb-5">
                    KEYWORDS: {{ song.keywords }}
                  </p></strong
                >
                <p class="fw-regular fs-12 text-black mb-5"></p>
                <div style="height: 80px">
                  <div
                    style="width: 90%; height: 5px;"
                    aria-valuenow="90"
                    aria-valuemin="0"
                    aria-valuemax="100"
                  >
                    <span v-html="song.url"></span>
                  </div>
                  <!-- <div class="card dark bg-inverse"> -->
                    <!-- <p class="text-primary mb-0"><strong>{{ user.artist_name }} said,</strong> -->
                    <p class="mb-20">"{{ song.description }}"</p>
                  <!-- </div> -->
                </div>
              </div>
              <!-- / box-description -->
            </div>
            <!-- / column -->
          </div>
          <!-- / row -->
        </div>
        <!-- box-w-image -->
      </div>
      <!-- / container -->
    </section>
    <!-- / about -->
    <!-- Comment Code Attempt -->
        <div class="comments comments-boxed bg-light">
            <h5 class="mb-3"></h5>
            <!-- comment form -->
            <div id="comment-form">
             <center> <h4 class="mb-3 text-primary mb-0">Give feedback on "{{ song.title }}".</h4><br></center>
                  <div class="card card-outline-primary">
                      <div class="card-body">
                        <form v-on:submit.prevent="createComment(song)" id="commentForm">
                            <div class="row">
                                <div class="col-md-6">
                                    <div class="form-group">
                                        NOTES: <textarea type="text" v-model="newCommentNotes" class="form-control border-faded" id="notes" placeholder="Drop a note if something sounds like it could be improved!"></textarea>
                                    </div>
                                    <span v-if="newCommentNotes.length > 0">
                                      <small>{{ 280 - newCommentNotes.length }} characters remaining.</small>
                                    </span>
                                </div><!-- / sub-column -->
                                <div class="col-md-6 sub-col-left" v-if="!$parent.isLoggedIn()">
                                    <div class="form-group">
                                        NAME: <input v-model="newCommentAuthor" type="text" class="form-control border-faded" id="author" placeholder="Author">
                                    </div>
                                </div><!-- / sub-column -->
                                <div class="card-body">
                                  TAGS: 
                                <div class="col-md-6">
                                  
                                  <br>
                                  <div v-for="tag in tags"> 
                                    <div class="list-checkbox">
                                        <div class="checkbox checkbox-primary">
                                            
                                              <input
                                                  :value="tag.id"
                                                  type="checkbox"
                                                  :id="tag.id"
                                                  v-model="tagIds"
                                                />
                                              <label :for="tag.id">{{ tag.name }}</label>
                                            
                                        </div>
                                        <br>
                                    </div>

                                  </div>
                                  </div>
                                </div><!-- / sub-column -->
                                <div class="col-md-6 sub-col-left">
                                    <div class="form-group">
                                        TIMESTAMP: <input id="song_timestamp" v-model="newSongTimestamp" class="form-control border-faded" placeholder="0:00 - 0:02">
                                    </div>
                                </div>
                            </div><!-- / row -->
                            <button type="submit" id="form-submit"  class="btn btn-primary pill m-1"><span>COMMENT</span></button>
                        </form><!-- / commentForm -->
                      </div>
                    </div>
            </div>
            <!-- / comment form -->

            <div class="spacer">&nbsp;</div>

            <div v-for="comment in song.comments">
              <div class="card">
                <div class="card-body">
                  <strong
                ><p>{{ comment.author }}</p></strong
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
