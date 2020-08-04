<template>
  <div class="hello">
    <p>{{error}}</p>

    <div class="div__post" v-for="post in post" :key="post.id">
      <h5>{{post.name}}</h5>
      <p>{{post.username}}</p>
      <p>{{post.email}}</p>
      <p>{{post.phone}}</p>
    </div>
  </div>
</template>

<script>
import TodoClass from "../TodoClass";
export default {
  name: "Todo",
  // Default data
  data() {
    return {
      post: [],
      error: "",
      text: ""
    };
  },

  // Created is same as React useEffect
  async created() {
    try {
      const tododata = await TodoClass.getPosts();
      this.post = tododata;
    } catch (error) {
      this.error = error;
    }
  },
  // This are customize functions
  methods: {
    // Create new todo
    async createPost() {
      const newTodo = await TodoClass.insertPost(this.text);
      this.text = newTodo;
    },
    // Delete new todo
    async deletePost(id) {
      const deleteTodo = await TodoClass.deletePost(id);
      this.post = deleteTodo;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
/* .hello {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  max-width: 50%;
} */
.div__post {
  min-height: 150px;
  background-color: lightgrey;
}
</style>
