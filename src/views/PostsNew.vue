<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newPostParams: {},
      errors: [],
    };
  },
  created: function () { },
  methods: {
    createPost: function () {
      axios
        .post("/posts.json", this.newPostParams)
        .then((response) => {
          console.log("posts create", response);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log("posts create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <h1>New post</h1>
    <form v-on:submit.prevent="createPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <p>
        Title:
        <input type="text" v-model="newPostParams.title" />
      </p>

      <p>
        Body:
        <input type="text" v-model="newPostParams.body" />
      </p>

      <p>
        Image:
        <input type="text" v-model="newPostParams.image" />
      </p>

      <input type="submit" value="Create" />
    </form>
  </div>
</template>