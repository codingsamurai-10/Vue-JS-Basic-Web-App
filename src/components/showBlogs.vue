<template>
  <div id="show-blogs" v-theme:column="'wide'">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="Search Blog" />
    <div class="single-blog" v-for="blog in filteredBlogs" :key="blog.id">
      <router-link :to="'/blog/' + blog.id"><h2>{{ blog.title | capitalize }}</h2></router-link>
      <article>{{ blog.content | snippet }}</article>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import searchMixin from "../mixins/searchMixin.js";

export default {
  components: {},

  data() {
    return {
      blogs: [],
      search: ""
    };
  },

  computed: {},

  mixins: [searchMixin],

  created() {
    axios.get("https://vue-js-playlist-87b19.firebaseio.com/posts.json").then((blogsData) => {
      return blogsData.data;
    }).then(data => {
      var blogsArray = [];
      for (let key in data) {
        data[key].id = key;
        blogsArray.push(data[key]);
      }
      this.blogs = blogsArray;
    });
  },

  filters: {
    capitalize: function(value) {
      return value.toUpperCase();
    }
  },

  directives: {
    rainbow: {
      bind(el, binding, vnode) {
        el.style.color =
          "#" +
          Math.random()
            .toString()
            .slice(2, 6);
      }
    },

    theme: {
      bind(el, binding, vnode) {
        if (binding.value == "wide") {
          el.style.maxWidth = "1200px";
        }
        if (binding.arg == "column") {
          el.style.background = "#ddd";
          el.style.padding = "20px";
        }
      }
    }
  }
};
</script>

<style scoped>
#show-blogs {
  max-width: 800px;
  margin: 0px auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>