<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      posts: []
    };
  },
  created: function () {
    console.log('in created');
    this.postsIndex();
  },
  methods: {
    postsIndex: function () {
      console.log('in posts...');
      axios.get(`/posts.json`).then(response => {
        console.log(response.data);
        this.posts = response.data
      })
    },

  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <br />
    <div v-for="post in posts" v-bind:key="post.id">
      <img v-bind:src="post.image" />
      <h2>
        Title: {{ post.id }}. {{ post.title }}
        <br />
        <br />
        Content: {{ post.body }}
      </h2>
      <br />
      <router-link v-bind:to="`/posts/${post.id}`">More details</router-link>
    </div>
  </div>
</template>

<style></style>
