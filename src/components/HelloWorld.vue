<template>
  <div class="hello">
    <div class="container-fluid">
      <div class="row">
        <div class="col-6" v-for="post in posts" :key="post.id">
          <div class="post" @click="$router.push(`/post/${post.id}`)">
            <h4>{{post.title}}</h4>
            <p>{{post.title}}</p>
            <h4><b>User Id: </b>{{post.userId}}</h4>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      posts: []
    }
  },
  created() {
    this.getPosts()
  },
  methods: {
    getPosts() {
      axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(res => {
        this.posts = res.data;
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.post {
  padding: 10px;
  border: 1px solid #ddd;
  margin-bottom: 10px;
  cursor: pointer;
}
</style>
