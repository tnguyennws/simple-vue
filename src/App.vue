<template>
  <div id="app">

    <div v-if="posts.length">
      <ul>
        <li
          v-for="post in posts"
          :key="post.id"
        >
          <h2>{{ post.title }}</h2>
          <p>{{ post.body }}</p>
        </li>
      </ul>
    </div>

    <div v-else>
      Chargement des posts…
    </div>

  </div>
</template>

<script>

export default {
  name: 'Simple Vue',
  data() {
    return {
      posts: []
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => {
      return response.json()
    })
    .then((result) => {
      this.posts = result
    })
    .catch(error => console.error(error))  
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
