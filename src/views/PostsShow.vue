<template>
  <div class="posts-show">
    <div>
      <router-link to="/posts">Back to all posts</router-link>
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <img :src="post.image" alt="" />
      <p></p>
      <li v-if="$parent.getUserId() == post.user_id">
        <router-link :to="`/posts/${post.id}/edit`">
          <button>Edit Post</button>
        </router-link>
      </li>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("posts/" + this.$route.params.id).then((response) => {
      this.post = response.data;
    });
  },
};
</script>
