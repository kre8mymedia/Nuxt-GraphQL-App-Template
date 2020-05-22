<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12 text-center">
        Does this work?
      </div>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'home',
  components: {

  },
  data() {
    return {
      categories: []
    }
  },
  apollo: {
    categories: gql`{
      categories {
        id
        name
      }
    }`,
  }
}
</script>


