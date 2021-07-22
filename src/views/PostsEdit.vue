<template>
  <div class="post-edit">
    <form v-on:submit.prevent="updatePost()">
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
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      errors: [],
      editPostParams: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      console.log(response.data);
      this.editPostParams = response.data;
    });
  },
  methods: {
    updatePost: function () {
      axios.patch("/posts/" + this.$route.params.id, this.editPostParams).then((response) => {
        console.log(response.data);
        this.$router.push("/posts/" + response.data.id);
      })
    }
  }
}
</script>
