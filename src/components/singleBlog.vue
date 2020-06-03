<template>
  <div id="single-blog">
    <h1>{{ blog.title }}</h1>
    <article>{{ blog.content }}</article>
    <p>Author: {{ blog.author }}</p>
    <ul>
        <li v-for="category in blog.categories" :key="category.id">{{ category }}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  components: {
      "axios": axios
  },
  data() {
    return {
      id: this.$route.params.id,
      blog: {}
    };
  },

  created() {
      axios.get("https://vue-js-playlist-87b19.firebaseio.com/posts/" + this.id + ".json").then((blogsData) => {
          return blogsData.data;
      }).then((data) => {
          this.blog = data;
      });
  }
};
</script>

<style scoped>
</style>
