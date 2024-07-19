<template>
  <v-form v-model="valid">
    <v-container  class="d-flex flex-column justify-center align-center vh-100 w-100 mt-15 mr-0">
      <v-col cols="10">
        <v-text-field
          v-model="email"
          :rules="emailRules"
          label="Email"
          hide-details
          required
          width="600"
        ></v-text-field>
      </v-col>

      <v-col cols="10">
        <v-text-field
          v-model="username"
          :rules="usernameRules"
          label="Username"
          hide-details
          required
          width="600"
        ></v-text-field>
      </v-col>

      <v-col cols="10">
        <v-text-field
          v-model="password"
          :rules="passwordRules"
          label="Password"
          hide-details
          required
          type="password"
          width="600"
        ></v-text-field>
      </v-col>

      <v-col >
        <v-btn class="ml-16 mt-16" @click="register" :disabled="!valid">Register</v-btn>
     
      </v-col>
      <v-btn class=" mt-0 ml-16" text color="primary"> <router-link to="/login">Already have an account?</router-link> </v-btn>
     
    </v-container>
   
  </v-form>
</template>

<script>
import axios from "axios";
import swal from "sweetalert";

export default {
  data() {
    return {
      valid: false,
      email: '',
      username: '',
      password: '',
      emailRules: [
        value => !!value || 'Email is required.',
        value => /.+@.+\..+/.test(value) || 'Email must be valid.',
      ],
      usernameRules: [
        value => !!value || 'Username is required.',
      ],
      passwordRules: [
        value => !!value || 'Password is required.',
      ],
    };
  },
  methods: {
    register() {
      if (this.valid) {
        axios.post("http://localhost:3005/register", {
          email: this.email,
          username: this.username,
          password: this.password
        })
        .then(response => {
          if (response.data.message) {
            swal("Error", response.data.message, "error");
          } else {
            swal("Account Created", "Your account has been created successfully!", "success")
            .then(() => {
              this.$router.push("/login");
            });
          }
        })
        .catch(error => {
          console.error("Error:", error);
          swal("Error", "An error occurred while registering", "error");
        });
      }
    }
  }
};
</script>
