<template>
  <footer>
      <slot name="title"></slot>
      <p>{{ copyright }} {{ title }}</p>
      <slot name="para"></slot>
  </footer>
</template>

<script>
import { bus } from '../main';

export default {
  props: {
      title: {
        type: String,
        required: true
      }
  },
  data () {
    return {
        copyright: "Copyright 2020"
    };
  },

  created() {
    bus.$on('titleChanged', (data) => {
      this.title = data;
    })
  }
}
</script>

<style scoped>
footer {
    background: #222;
    padding: 6px;
}

p {
    color: lightgreen;
    text-align: center;
}
</style>
