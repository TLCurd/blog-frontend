<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newUserParams: {
        name: "",
        email: "",
        password: "",
        password_confirmation: ""
      },
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newUserParams.name" /> <br />
        <small v-if="newUserParams.name.length <= 14 && newUserParams.name.length > 0">{{
          20 - newUserParams.name.length
        }} characters remaining</small>
        <small v-if="newUserParams.name.length >= 15 && newUserParams.name.length <= 20" class="text-warning">{{
          20 -
          newUserParams.name.length
        }} characters remaining</small>
        <small v-if="newUserParams.name.length > 20" class="text-danger">username too long</small>
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="newUserParams.email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="newUserParams.password" />
      </div>
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newUserParams.password_confirmation" />
        <br />
        <small v-if="newUserParams.password_confirmation !== newUserParams.password" class="text-danger">Passwords don't
          match</small>
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>