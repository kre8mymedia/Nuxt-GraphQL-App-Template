<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxt-graphql
      </h1>
      <button @click="handleClick">Test Mutation</button>
      <h2 class="subtitle">
        nuxt &amp; graphql app
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import gql from 'graphql-tag'

export default {
  apollo: {
    posts: gql`
    {
      posts {
        id
        title
        author {
          name
        }
        comments {
          id
          reply
        }
      }
    }`,
  },
  methods: {
    handleClick() {
      try {
        this.$apollo.mutate({
          // Query
          mutation: gql`mutation {
            createUser(name: "Hale Brown", email: "sk8er71091@netscape.net", password: "johnryan92") {
              id
              name
            }
          }`,
        })
      } catch (e) {
        console.error(e)
      }
    }
  },
  components: {
    Logo
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
