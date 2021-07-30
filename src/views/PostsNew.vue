<template>
  <div class="post-new">
    <img v-if="status" :src="`https://http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="createPost()">
      <h1>Create Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
        <small>{{ 100 - newPostParams.body.length }} characters remaining</small>
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input v-if="newPostParams.body.length < 100" type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      errors: [],
      newPostParams: { body: "" },
      status: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/");
        })
        .catch((error) => {
          this.status = error.response.status;
        });
    },
  },
};
</script>

<style>
img {
  width: 50%;
}
</style>
