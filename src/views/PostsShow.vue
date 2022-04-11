<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the show!",
      post: {},
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      console.log("showing product...");
      console.log(this.$route.params.id);
      axios.get(`/posts/${this.$route.params.id}.json`).then(response => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
}  
</script>

<template>
  <div class="post-show">
    <h2>{{ post.title }}</h2>
    <img v-bind:src="post.image" v-bind:alt="post.title" />
    <p>Body: {{ post.body }}</p>
    <router-link to="/posts">Back to all posts</router-link>
  </div>
</template>
