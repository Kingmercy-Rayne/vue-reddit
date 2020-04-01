<template>
  <div class="hello">
    <h1>Reddit</h1>
  </div>
</template>

<script>
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
      const posts = [];
      const url = 'https://www.reddit.com/r/programmerhumor/new.json?Limit=100';
      fetch(url)
        .then((response) => response.json())
        .then((result) => {
          posts.push(result.data.children);
          console.log(posts);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
