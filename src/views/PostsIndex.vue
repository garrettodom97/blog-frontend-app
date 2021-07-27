<template>
  <div class="posts">
    <h1>Posts</h1>
    <div class="cards">
      <div
        v-for="post in posts"
        v-bind:key="post.id"
        :class="{ selected: post === currentPost }"
        v-on:mouseover="currentPost = post"
      >
        <router-link class="routerLink" v-bind:to="`/posts/${post.id}`">
          <div class="card mb-3" style="max-width: 540px">
            <div class="row no-gutters">
              <div class="col-md-4">
                <img :src="post.image" alt="No Image Found" />
              </div>
              <div class="col-md-8">
                <div class="card-body">
                  <h5 class="card-title">{{ post.title }}</h5>
                  <p class="card-text">
                    {{ post.body }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
      currentPost: {},
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>

<style>
.routerLink {
  text-decoration: none;
  color: black;
}

.cards {
  align-content: center;
}

.selected {
  background-color: cadetblue;
}
</style>
