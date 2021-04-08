<template>
  <div id="app">
    <div v-if="posts.length">
      {{ posts }}
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
      posts: [
        {
          id: 1,
          title: "Hello",
          body: "Hello world"
        },
        {
          id: 2,
          title: "Un autre article",
          body: "Contenu de cet article."
        }
      ]
    }
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
