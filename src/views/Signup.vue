<template>
  <div class="signup">
    <!-- <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>Signup</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Email:</label>
          <input type="email" class="form-control" v-model="email" />
        </div>
        <div class="form-group">
          <label>Password:</label>
          <input type="password" class="form-control" v-model="password" />
        </div>
        <div class="form-group">
          <label>Password confirmation:</label>
          <input
            type="password"
            class="form-control"
            v-model="passwordConfirmation"
          />
        </div>
        <input type="submit" class="btn btn-primary pill m-1" value="Submit" />
      </form>
    </div> -->

    <div class="col-sm-6">
      <p class="lead mt-3 mb-3"></p>
      <div class="card">
        <div class="card-body">
          <form
            class="validation-inner"
            id="register-form"
            v-on:submit.prevent="submit()"
          >
            <h5 class="mb-40">Register</h5>
            <ul>
              <li class="text-danger" v-for="error in errors">{{ error }}</li>
            </ul>
            <div class="form-group">
              <input
                type="email"
                class="form-control"
                name="emailRegister"
                placeholder="Email"
                v-model="email"
              />
            </div>
            <!-- / form-group -->
            <div class="form-group">
              <input
                type="text"
                class="form-control"
                name="usernameRegister"
                placeholder="Username"
                v-model="user.artist_name"
                required
              />
            </div>
            <!-- / form-group -->
            <div class="form-group">
              <input
                type="password"
                id="passwordRegister"
                class="form-control"
                name="passwordRegister"
                placeholder="Password"
                v-model="password"
              />
            </div>
            <!-- / form-group -->
            <div class="form-group">
              <input
                type="password"
                class="form-control"
                name="passwordRegisterConfirm"
                placeholder="Confirm Password"
                v-model="passwordConfirmation"
                required
              />
            </div>
            <!-- / form-group -->

            <div class="row v-center">
              <div class="col-lg-7 tablet-lg-top">
                <div class="checkbox checkbox-primary ml-5">
                  <label class="hidden"><input type="checkbox"/></label>
                  <input id="checkbox2" type="checkbox" />
                  <label for="checkbox2"
                    ><span><a href="#x">Terms & Conditions</a></span></label
                  >
                </div>
                <!-- / checkbox -->
              </div>
              <!-- / column -->

              <div class="col-lg-5 text-right">
                <button
                  type="submit"
                  class="btn btn-md btn-primary tablet-lg-fw"
                >
                  Register
                </button>
              </div>
              <!-- / column -->
            </div>
            <!-- / row -->
          </form>
          <!-- / register-form -->
        </div>
        <!-- / card-body -->
      </div>
      <!-- / card -->
    </div>
    <!-- col-sm-6 -->
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
      email: "",
      password: "",
      passwordConfirmation: "",
      errors: [],
      artist_name: "",
    };
  },
  methods: {
    submit: function() {
      var params = {
        artist_name: this.user.artist_name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post("/api/users", params)
        .then((response) => {
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
