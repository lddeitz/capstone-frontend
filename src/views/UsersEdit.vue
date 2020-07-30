<template>
  <div class="users-edit">
    <h2>Edit Your Profile</h2>

    <div class="edit-form">
      <form v-on:submit.prevent="editAccount()">  
        <label for="artist_name">Artist Name:</label>
        <input type="text" v-model="user.artist_name"><br>

        <label for="first_name">First Name:</label>
        <input type="text" v-model="user.first_name"><br>

        <label for="last_name">Last Name:</label>
        <input type="text" v-model="user.last_name"><br>

        <label for="bio">Bio:</label>
        <input type="text" v-model="user.bio"><br>

        <label for="email">Email:</label>
        <input type="text" v-model="user.email"><br>

        <label for="email">Password:</label>
        <input type="text" v-model="user.password"><br>

        <input type="submit" value="Update"><br>
      </form>
    </div>

    <!-- <div class="edit-img">
      <img :src="user.profile_picture" alt="profile_picture"><br>
      <label>Image</label>
      <input type="file" v-on:change="setFile($event)" ref="fileInput">
    </div> -->

    <div class="delete-account">
      <button v-on:click="deleteAccount()">Delete Account</button>
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
      // user_id: this.user.id
      user_id: localStorage.getItem("user_id")
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.user = response.data;
      console.log(this.user);
    });
  },
  methods: {
    // setFile: function(event) {
    //   if (event.target.files.length > 0) {
    //     this.image = event.target.files[0];
    //   }
    // },
    editAccount: function() {
      var params = {
        artist_name: this.user.artist_name,
        first_name: this.user.first_name,
        last_name: this.user.last_name,
        bio: this.user.bio,
        email: this.user.email,
        password: this.user.password
        // profile_picture: this.user.profile_picture
      };
      axios
        .patch(`/api/users/${this.user.id}`, params)
        .then(response => {
          // console.log(response.data);
          // this.user = response.data;
          this.$router.push(`/users/${this.user.id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
    deleteAccount: function() {
      if (confirm("Are you sure you want to delete your account?")) {
        axios.delete(`/api/users/${this.user.id}`).then(response => {
          console.log("Account deleted.", response.data);
          this.$router.push("/signup");
        });
      }
    }
  }
};
</script>

<style>
</style>