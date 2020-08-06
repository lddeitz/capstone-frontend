<template>
  <div class="container">
    <div class="login">
      <!-- <form v-on:submit.prevent="submit()">
        <h1>Login</h1>
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

        <input class="btn btn-primary pill m-1" type="submit" value="Submit" />
      </form>

    </div>
  </div> -->

      <!-- login-form -->

      <center>
        <div class="col-sm-6">
          <p class="lead mt-3 mb-3"></p>
          <div class="card">
            <div class="card-body">
              <form
                v-on:submit.prevent="submit()"
                class="validation-inner"
                id="login-form"
              >
                <h5 class="mb-40">Log In</h5>
                <div class="form-group">
                  <input
                    type="text"
                    class="form-control"
                    name="emailLogin"
                    placeholder="Email"
                    v-model="email"
                  />
                </div>
                <!-- / form-group -->

                <div class="form-group">
                  <input
                    type="password"
                    class="form-control"
                    name="passwordLogin"
                    placeholder="Password"
                    required
                    v-model="password"
                  />
                </div>
                <!-- / form-group -->

                <!-- <div class="row v-center mt-15"> -->
                <div class="col-lg-7 tablet-lg-top">
                  <div class="checkbox checkbox-primary ml-5">
                    <!-- <label class="hidden"><input type="checkbox"/></label> -->
                    <!-- <input id="checkbox1" type="checkbox" /> -->
                    <!-- <label for="checkbox1"> -->
                    <!-- <span class="fw-light">Remember Me</span> -->
                    <!-- </label> -->
                  </div>
                  <!-- / checkbox -->
                </div>
                <!-- / column -->
                <!-- <div class="col-lg-5 text-right"> -->
                <center>
                  <button
                    type="submit"
                    class="btn btn-md btn-primary tablet-lg-fw"
                  >
                    Login
                  </button>
                </center>
                <!-- </div> -->
                <!-- / column -->
                <!-- </div> -->
                <!-- / row -->

                <!-- <div class="mt-15">
                    <a href="#x" class="forgot-password">Forgot your Password?</a>
                  </div> -->
                <!-- / mt-15 -->
              </form>
              <!-- / login-form -->
            </div>
            <!-- / card-body -->
          </div>
          <!-- / card -->
        </div>
        <!-- / col-sm-6 -->
      </center>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      email: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("/api/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          localStorage.setItem("user_id", response.data.user_id);
          this.$router.push(`/users/${response.data.user_id}`);
        })
        .catch((error) => {
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>
