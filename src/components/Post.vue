<template>
  <div class="hello">
    <div class="container-fluid">
      <div class="row">
          <div class="col-12">
              <button @click="$router.push('/')">Back</button>
              <br><br><br>
          </div>
        <div class="col">
            <div class="post-block">
                <h4>{{post.title}}</h4>
                <p>{{post.title}}</p>
                <h4><b>User Id: </b>{{post.userId}}</h4>
            </div>
            <br><br><br>
            <div class="post-block">
                <p><b>ID:</b> {{user.id}}</p>
                <p><b>Name:</b> {{user.name}}</p>
                <p><b>Username:</b> {{user.username}}</p>
                <p><b>Email:</b> {{user.email}}</p>
            </div>
            <br><br><br>
            <div class="post-block">
                <div class="comment" v-for="comment in comments" :key="comment.id">
                    <h4>{{comment.name}}</h4>
                    <p>{{comment.body}}</p>
                    <p><b>User:</b>{{comment.email}}</p>
                </div>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Post',
  props: ['id'],
  data () {
    return {
      post: {},
      user: {},
      comments: [],
    }
  },
  created() {
    this.getPost()
  },
  methods: {
    getPost() {
      axios.get(`https://jsonplaceholder.typicode.com/posts/${this.id}`)
      .then(res => {
        this.post = res.data;
        this.getComments()
      })
    },
    getComments() {
      axios.get(`https://jsonplaceholder.typicode.com/posts/${this.id}/comments`)
      .then(res => {
        this.comments = res.data;
        this.getUser()
      })
    },
    getUser() {
      axios.get(`https://jsonplaceholder.typicode.com/users/${this.post.userId}`)
      .then(res => {
        this.user = res.data;
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.post-block {
  padding: 10px;
  border: 1px solid #ddd;
  margin-bottom: 10px;
}
.comment {
  border: 1px solid #ddd;
  padding: 5px;

}
</style>
