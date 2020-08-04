<template>
  <div class="users-edit">
    <!-- <h2>Edit Your Profile</h2> -->
    <div class="container">
      <div class="spacer-2x">&nbsp;</div>
      <h2 class="section-title text-center mb-10">EDIT PROFILE</h2>
      <div class="spacer-line border-primary">&nbsp;</div>
      <div class="spacer-2x">&nbsp;</div>
    </div>
    <!-- / container -->

    <!-- <div class="edit-form">
      <form v-on:submit.prevent="editUser()">
        <label for="artist_name">Artist Name:</label>
        <input type="text" v-model="user.artist_name" /><br />
        <label for="first_name">First Name:</label>
        <input type="text" v-model="user.first_name" /><br />
        <label for="last_name">Last Name:</label>
        <input type="text" v-model="user.last_name" /><br />
        <label for="bio">Bio:</label>
        <input type="text" v-model="user.bio" /><br />
        <label for="email">Email:</label>
        <input type="text" v-model="user.email" /><br />
        <label for="email">Password:</label>
        <input type="text" v-model="user.password" /><br />
        Update Profile Picture
        <input
          type="file"
          v-on:change="setFile($event)"
          ref="fileInput"
        /><br />
        <input
          type="submit"
          class="btn btn-primary pill m-1"
          value="Update"
        /><br />
      </form>
    </div> -->

    <div class="container">
      <div class="row mb-30">
        <div class="col-6">
          <p class="lead mt-3 mb-3"></p>
          <form
            class="validation-inner"
            v-on:submit.prevent="editUser()"
            id="form-validation"
          >
            <div class="form-group">
              Username:
              <input
                type="text"
                class="form-control"
                id="username"
                name="inputUsername"
                placeholder="Username"
                v-model="user.artist_name"
              />
            </div>
            <!-- / form-group -->
            <div class="row mb-30">
              <div class="col-6">
                <div class="form-group">
                  First Name:
                  <input
                    type="text"
                    class="form-control"
                    id="firstname"
                    name="inputFirstName"
                    placeholder="First Name"
                    v-model="user.first_name"
                    required
                  />
                </div>
              </div>
              <!-- / form-group -->
              <div class="col-6">
                <div class="form-group">
                  Last Name:
                  <input
                    type="text"
                    class="form-control"
                    id="lastname"
                    name="inputLastName"
                    placeholder="Last Name"
                    v-model="user.last_name"
                  />
                </div>
              </div>
            </div>
            <!-- / form-group -->
            <div class="form-group">
              Bio:
              <textarea
                id="bio"
                class="form-control"
                name="inputBio"
                rows="5"
                placeholder="Bio"
                v-model="user.bio"
                required
              ></textarea>
            </div>
            <!-- / form-group -->
            <div class="form-group">
              Email:
              <input
                type="text"
                class="form-control"
                id="email"
                name="inputEmail"
                placeholder="Email"
                v-model="user.email"
              />
            </div>
            <!-- / form-group -->
            <div class="form-group">
              Password:
              <input
                type="text"
                class="form-control"
                id="password"
                name="inputPassword"
                placeholder="Password"
                v-model="user.password"
              />
            </div>
            <!-- / form-group -->
            <button type="submit" class="btn btn-primary pill m-1">
              Update
            </button>
          </form>
        </div>
        <!-- / col-sm-6 -->
        <div class="col-6">
          <center>
            <img
              class="figure-img img-fluid circle w-50 raised move"
              :src="user.profile_picture"
              alt="profile_picture"
            />
          </center>
          <div class="form-group">
            <center>
              <input
                type="file"
                id="artwork"
                name="inputProfilePicture"
                placeholder="ProfilePicture"
                v-on:change="setFile($event)"
                ref="fileInput"
              />
            </center>
          </div>
          <!-- / form-group -->
        </div>
      </div>
    </div>
    <div class="spacer">&nbsp;</div>

    <div class="spacer">&nbsp;</div>

    <center>
      <div class="delete-account">
        <button class="btn btn-danger-gradient m-10" v-on:click="deleteUser()">
          DELETE ACCOUNT
        </button>
      </div>
    </center>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      errors: [],
      user: {},
      user_id: localStorage.getItem("user_id"),
      // artist_name: "",
      // first_name: "",
      // last_name: "",
      // bio: "",
      profile_picture: "",
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      // console.log(response.data);
      this.user = response.data;
      console.log(this.user);
    });
  },
  methods: {
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.user.profile_picture = event.target.files[0];
      }
    },
    editUser: function() {
      var formData = new FormData();
      formData.append("artist_name", this.user.artist_name);
      formData.append("first_name", this.user.first_name);
      formData.append("last_name", this.user.last_name);
      formData.append("bio", this.user.bio);
      formData.append("email", this.user.email);
      formData.append("password", this.user.password);
      if (this.user.profile_picture) {
        formData.append("profile_picture", this.user.profile_picture);
      }
      axios
        .patch(`/api/users/${this.user.id}`, formData)
        .then((response) => {
          // console.log(response.data);
          this.user = response.data;
          this.$router.push(`/users/${this.user.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
      // var params = {
      //   artist_name: this.user.artist_name,
      //   first_name: this.user.first_name,
      //   last_name: this.user.last_name,
      //   bio: this.user.bio,
      //   email: this.user.email,
      //   password: this.user.password
      //   profile_picture: this.user.profile_picture
      // };
      // },
      // updateProfilePicture: function() {
      //   var formData = new FormData();
      //   formData.append("img_url", this.user.img_url);
      //   axios
      //     .patch(`/api/users/${this.user.id}`, formData)
      //     .then(response => {
      //       // console.log(response.data);
      //       // this.user = response.data;
      //       this.$router.push(`/users/${this.user.id}`);
      //     })
      //     .catch(error => {
      //       this.errors = error.response.data.errors;
      //     });
    },
    deleteUser: function() {
      if (confirm("Are you sure you want to delete your account?")) {
        axios.delete(`/api/users/${this.user.id}`).then((response) => {
          console.log("Account deleted.", response.data);
          this.$router.push("/signup");
        });
      }
    },
  },
};
</script>

<style></style>
