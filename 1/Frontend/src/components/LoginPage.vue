<template>
  <v-form  v-model="valid">
    <v-container  class="d-flex flex-column justify-center align-center mt-15" >
      <v-row   width="00" justify="center">
        <v-col cols="10">
          <v-text-field
            v-model="username"
            :rules="usernameRules"
            label="Username"
            hide-details
            required
          ></v-text-field>
        </v-col>

        <v-col cols="10" >
          <v-text-field
            v-model="password"
            :rules="passwordRules"
            label="Password"
            hide-details
            required
            type="password"
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="6" class="text-center mt-4">
          <v-btn @click="login" :disabled="!valid">Login</v-btn>
        </v-col>

        <v-col cols="12" md="6" class="text-center mt-2">

          <v-btn>     <router-link to="/SignUp">Don't have an account?</router-link>  </v-btn>
      
        </v-col>
      </v-row>
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
      username: '',
      password: '',
      usernameRules: [
        value => !!value || 'Username is required.',
      ],
      passwordRules: [
        value => !!value || 'Password is required.',
      ]
    };
  },
  methods: {
    login() {
      if (this.valid) {
        axios.post("http://localhost:3005/login", {
          username: this.username,
          password: this.password,
        }).then((response) => {
          if (response.data.message) {
            swal("Error", response.data.message, "error");
          } else {
            const userEmail = response.data[0].username;
            swal("Login Successful", `Welcome, ${userEmail}!`, "success").then(() => {
              this.$router.push("/");
            });
          }
        }).catch(error => {
          console.error("Error:", error);
          swal("Error", "An error occurred while logging in", "error");
        });
      }
    }
  }
};
</script>
