<template>
  <div class="hello mt-3">
    <ul class="list-unstyled">
      <li v-for="(post, index) in posts" :key="index" class="media mt-3">
        <img class="mr-3" :src="post.data.thumbnail" alt="post img" />
        <div class="media-body">
          <h5 class="mt-0 mb-1">{{ post.data.title }}</h5>
          <p>
            <span class="badge badge-pill badge-secondary">
              {{ post.data.num_comments }} comments
            </span>
          </p>
          <span>created {{ formatDate() }}</span>
        </div>
        <h4 class="text-danger">{{ post.data.ups }}</h4>
      </li>
    </ul>
  </div>
</template>

<script>
// import {distanceInWordsToNow } from 'date-fns';
import distanceInWordsToNow from 'date-fns/distance_in_words_to_now'

export default {
  name: 'Posts',
  data() {
    return {
      posts: [],
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      const url = 'https://www.reddit.com/r/programmerhumor/new.json?Limit=100';
      fetch(url)
        .then((response) => response.json())
        .then((result) => {
          this.posts = result.data.children;
          console.log(this.posts);
        });
    },
    formatDate() {
      return distanceInWordsToNow(new Date(2014, 6, 2));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ups {
  color: red;
}
</style>
