<script>
// make proper request to backend
// prefill in data about this Post
import axios from "axios";
export default {
  data: function () {
    return {
      editPostParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .patch(`/posts/${this.$route.params.id}.json`, this.editPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/posts/${this.$route.params.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}.json`).then(response => {
      console.log(response.data);
      this.editPostParams = response.data;
    })
  }
};
</script>


<template>
  <div class="posts-edit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="editPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="editPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
    <a v-bind:href="`posts/${editPostParams.id}`">Show Post</a>
  </div>
</template>