<template>
  <div class="users-show">
    <body>
      <div class="container">
        <div class="spacer-2x">&nbsp;</div>
        <h2 class="section-title text-center mb-10">
          <div class="container">
            <!-- <img
              class="figure-img img-fluid circle w-75"
              style="max-width:10%; max-height:10%;"
              v-if="user.profile_picture"
              :src="user.profile_picture"
              :alt="user.artist_name"
            /> -->

            <!-- / column -->
          </div>
          <center>
            <div class="col-md-3 card card-rounded">
              <div class="widget text-center p-30 bg-white">
                <img
                  :src="user.profile_picture"
                  alt=""
                  class="circle w-50 mb-15"
                />
                <h6 class="widget-title">{{ user.artist_name }}</h6>
                <p
                  class="fs-12 post-meta-small pt-15 pb-15 mt-15 mb-15 border-faded"
                >
                  {{ user.first_name }} {{ user.last_name }}
                </p>
                <p class="mb-0">{{ user.bio }}</p>
              </div>
              <!-- / widget -->
            </div>
            <!-- / column -->
          </center>
        </h2>
        <!-- <div class="spacer-line border-primary">&nbsp;</div>
        <div class="spacer-2x">&nbsp;</div> -->
        <center></center>
        <div class="spacer-2x">&nbsp;</div>
      </div>

      <!-- <div class="col-md-4">
                <div class="card card-rounded text-center">
                    <div class="card-body">
                        <i class="ti-quote-right fs-18 card-icon-tag text-warning"></i>
                        <img src="assets/images/placeholder-square.jpg" alt="" class="promo-box-image circle mt-20 mb-15">
                        <p class="mb-0 fs-18">Erika Doe</p>
                        <p class="fs-12 post-meta-small pt-15 pb-15 mt-15 mb-15 border-faded"><i class="ti-calendar text-success"></i> 21 Jan 2020 <span class="mr-5 ml-5 text-muted">/</span> <i class="ti-bookmark text-warning"></i> Photography</p>
                        <p class="mb-0 fs-14">"Fusce imperdiet sollicitudin scelerisque. Etiam tristique eu nisl ut dapibus. Donec et vehicula cursus pretium."</p>
                        <a href="#x" class="btn btn-sm btn-warning pill mt-20"><i class="ti-book ti-12 va-middle mr-5"></i> <span class="va-middle">READ MORE</span></a>
                    </div>
                </div>
            </div> -->

      <!-- <div class="col-md-4">
                <div class="promo-box promo-center">
                     <div class="promo-container-big-md">
                        <div class="promo-big">
                            <img src="assets/images/placeholder-square.jpg" alt="" class="promo-box-image img-md circle mb-25">
                        </div>
                        <h6 class="box-title mb-15">CENTER MEDIUM</h6>
                        <p class="box-description">Quisque in suscipit nulla. Maecenas id pulvinar est. Sed euismod hendrerit.</p>
                    </div>
                </div>
            </div> -->

      <!-- <div class="artist-info">
        <h2>{{ user.artist_name }}</h2>

        <div class="col-md-4">
          <div class="">
            <div class="card-body text-center">
              <img
                class="mb-30 circle"
                style="max-width:65%;"
                v-if="user.profile_picture"
                :src="user.profile_picture"
                :alt="user.artist_name"
              />
              <h6 class="card-title mb-10">{{ user.artist_name }}</h6>
              <p class="mb-0 fs-15 fw-regular">
                {{ user.first_name }} {{ user.last_name }}
              </p>
              <p class="card-text mb-30">{{ user.bio }}</p>
              <p class="mb-0">
                <router-link
                  class="btn btn-primary pill m-1"
                  :to="`/users/${user.id}/edit`"
                  >Edit Profile</router-link
                >
              </p>
            </div>
          </div>
        </div>
      </div>

      <div v-for="song in user.songs">
        <div class="col-md-3">
          <router-link :to="`/songs/${song.id}/`">
            <center>
              <p class="lead mt-3 mb-3">{{ song.title }}</p>
            </center>
            <center>
              <img
                :src="song.img_url"
                class="figure-img img-fluid rounded w-75 raised move"
                :alt="`${song.title}`"
              />
            </center>
          </router-link>
          <center>
            <router-link class="btn btn-success m-1" :to="`/songs/${song.id}/`"
              >VIEW</router-link
            >
          </center>
        </div>

        <router-link
          class="btn btn-primary pill m-1"
          :to="`/songs/${song.id}/edit`"
          >Edit Song</router-link
        >
      </div> -->
      <section id="shop" class="lg bg-white pb-70">
        <div class="container">
          <div class="container">
            <h2 class="section-title text-center mb-10">SONGS</h2>
            <div class="spacer-line border-primary">&nbsp;</div>
            <div class="spacer-2x">&nbsp;</div>
          </div>
          <!-- <div class="section-heading text-center">
            <div class="widget text-center p-y-10"> -->
          <!-- <router-link :to="`/users/${user.id}/edit`">
                <img
                  v-if="user.profile_picture"
                  :src="user.profile_picture"
                  :alt="user.artist_name"
                  class="circle w20 mb-15"
                />
              </router-link>
              <h2 class="mb-15">{{ user.artist_name }}</h2>
              <p class="mb-0 fs-15 fw-regular">
                {{ user.first_name }} {{ user.last_name }}
              </p>
              <p class="w50 mb-70 m-x-auto">
                {{ user.bio }}
              </p> -->
          <!-- </div>
          </div> -->
          <!-- / section-heading -->
          <h2></h2>

          <div class="row">
            <div class="col-sm-6 col-md-3 mb-30">
              <div v-for="song in user.songs">
                <div class="product text-center">
                  <p class="mb-1">
                    <span class="song title"
                      ><a
                        :href="`/songs/${song.id}/`"
                        class="card-title fs-18 fw-regular title-link"
                        >{{ song.title }}</a
                      ></span
                    >
                  </p>
                  <!-- / sale-badge -->
                  <div class="container">
                    <router-link :to="`/songs/${song.id}/`">
                      <img
                        :src="song.img_url"
                        alt=""
                        class="mb-30 rounded raised"
                      />
                    </router-link>
                  </div>
                  <router-link
                    class="btn btn-success m-1"
                    :to="`/songs/${song.id}/`"
                    >VIEW</router-link
                  >
                  <!-- <router-link
                    class="btn btn-primary pill m-2"
                    :to="`/songs/${song.id}/edit`"
                    >EDIT</router-link
                  > -->
                  <div class="spacer-2x">&nbsp;</div>
                </div>
                <!-- / product -->
              </div>
            </div>
            <!-- / column -->
          </div>
          <!-- / row -->
        </div>
        <!-- / container -->
      </section>
      <!-- / shop -->
    </body>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      user: {},
      song_id: "",
      userSongs: null,
      songs: [],
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
      console.log(this.user);
    });
  },
  methods: {
    editRedirect() {
      axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
        this.$router.push(`/users/${response.data.user_id}/edit`);
      });
    },
    newSongRedirect() {
      axios.post("/api/songs/").then((response) => {
        this.$router.push("/songs/new");
      });
    },
    editSongRedirect() {
      axios.get(`/api/songs/${this.$route.params.id}`).then((response) => {
        this.$router.push(`/songs/${this.$route.params.id}/edit`);
      });
    },
  },
};
</script>
