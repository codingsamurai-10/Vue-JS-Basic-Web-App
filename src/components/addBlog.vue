<template>
  <div id="add-blog">
      <h2>Add new blog</h2>

      <form v-if="!submitted">
          <label>Blog title</label>
          <input type="text" v-model.lazy="blog.title">
      
          <label>Blog content</label>
          <textarea v-model.lazy="blog.content"></textarea>

          <div id="checkboxes">
              <label>Ninjas</label>
              <input type="checkbox" value="Ninjas" v-model="blog.categories">
              <label>Wizards</label>
              <input type="checkbox" value="Wizards" v-model="blog.categories">
              <label>Mario</label>
              <input type="checkbox" value="Mario" v-model="blog.categories">
              <label>Cheese</label>
              <input type="checkbox" value="Cheese" v-model="blog.categories">
          </div>

          <label>Author</label>
          <select v-model="blog.author">
              <option v-for="auth in authors" :key="auth.id">{{auth}}</option>
          </select>
          
          <button @click.prevent="postData">Add blog</button>
      </form>

      <div v-if="submitted">Thanks for posting!</div>
      <button v-show="submitted" @click="submitted = false">Add Another</button>

      <div id="preview">
          <h3>Preview blog</h3>
          <p>Blog title: {{ blog.title }} </p>
          <p>Blog content:</p>
          <p>{{ blog.content }}</p>
          <p>Blog categories:</p>
          <ul>
              <li v-for="el in blog.categories" :key="el.id">{{el}}</li>
          </ul>
          <p>Author: {{blog.author}}</p>
      </div>
  </div>
</template>

<script>
import Axios from 'axios';

export default {
  components: {},

  data() {
    return {
        blog: {
            title: "",
            content: "",
            categories: [],
            author: ""
        },
        authors: ["Ninja", "Angluar", "Vue"],
        submitted: false
    };
  },

  methods: {
      postData: function () {
          Axios.post("https://vue-js-playlist-87b19.firebaseio.com/posts.json", this.blog).then(function (data) {
          });
          this.submitted = true;
      }
  }
};
</script>

<style scoped>
#add-blog *{
    box-sizing: border-box;
}
#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px solid #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}

#checkboxes input {
    display: inline-block;
    margin-right: 10px;
}

#checkboxes label {
    display: inline-block;
}
</style>
