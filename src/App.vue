<template>
  <div id="app">
    <h1>Articles</h1>
    <!--
    Des propriétés de composants sont définies (`:totalPages` et `:perPage`)
    et de valeurs sont transmissent (`totalPages` et `perPage`) à ce composant.
    Un écouteur d'évenement `v-on:` est spécifié pour surveiller `load-pages`, lorsque celui-ci sera déclenché, il appellera la méthode `loadPage`. Notez que les paramètres associés à cet évenemnt (`page.id`) seront transmis à la méthode-->
    <Pagination
      :totalPages="totalPages"
      :perPage="perPage"
      v-on:load-page="loadPosts"
    />
 
    <div v-if="isLoading">
      <p>
        Chargement des posts…
      </p>
    </div>

    <div v-else>
      <article class="article">
        <li v-for="post in posts" :key="post.id">
          <a :href="post.link">
            <h2 v-html="post.title.rendered"></h2>
          </a>
          <p v-html="post.excerpt.rendered"></p>
        </li>
      </article>
    </div>

  </div>
</template>

<script>
/** WP API avec pagination **/
import Pagination from '@/components/Pagination.vue'
//import Article from '@/components/Article.vue'
export default {
  name: 'SimpleVuePagination',
  components: {
    Pagination
  },
  data() {
    return {
      posts: [],
      isLoading: true,
      perPage: 10,
      totalPages: 0,
    }
  },
  mounted() {
     this.loadPosts(1)
  },
  /**
   * Nous utilisons uen méthode, plutôt que d'éxéuter l'appel avec `mounted`
   * Ceci nous permet réemployer cette méthde à chaque clique sur un des 
   * bouton de la pagination
   */
  methods: {
    loadPosts(currentPage) {
      this.isLoading = true
      // N'hésitez pas à utiliser une autre source de données WP
      fetch('https://relikto.com/wp-json/wp/v2/posts?' + new URLSearchParams({
        context: 'view',
        page: currentPage,
        per_page: this.perPage,
      }), {
        method: 'GET',
      })
        .then(response => {
          this.totalPages = parseInt(response.headers.get('X-WP-TotalPages'))
          return response.json()
        })
        .then(json => {
          this.posts = json
          this.isLoading = false
        })
    }
  }
}
</script>

<style>

/**
 * Ce style peut éventuellement être placé dans le fichier
 * de style global `assets/styles.css`
 */

#app {
  font-family: cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #090909;
  max-width: 35rem;
  margin: 0 auto;
}
.article {
  list-style: none;
  padding-left: 0;
}

h1{
  font-family: cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #19516D;
}

</style>