<template>
  <div class="users-edit">
    <h2>Edit Your Profile</h2>

    <div class="edit-form">
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
    </div>

    <img
      class="profile picture"
      :src="user.profile_picture"
      alt="profile_picture"
    />

    <div class="delete-account">
      <button v-on:click="deleteUser()">Delete Account</button>
    </div>
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
