<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      console.log("post show", response);
      this.post = response.data;
    });
  },
  methods: {},
};
</script>

<template>
  <div class="post-show">
    <h2>{{ post.title }}</h2>
    <img v-bind:src="post.image" v-bind:alt="post.title" />
    <p>Body: {{ photo.width }}</p>
    <router-link to="/posts">Back to all posts</router-link>
  </div>
</template>
