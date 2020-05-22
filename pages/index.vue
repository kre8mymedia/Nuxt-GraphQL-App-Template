<template>
  <div class="container-fluid">
    
    <div class="row">
      <div class="col-12 text-center pt-4">
        <!-- CATEGORIES -->
        <ApolloQuery :query="categoriesQuery">
          <template slot-scope="{ result: { data, loading }, isLoading }">
            <div v-if="isLoading">Loading...</div>
            <div v-else>
              <a @click.prevent="selectCategory('all')" href="#" class="category">All</a>
              <a @click.prevent="selectCategory('featured')" href="#" class="category">Featured</a>
              <a @click.prevent="selectCategory(category.id)" href="#" :key="category.id" class="category" v-for="category of data.categories">
                {{ category.id }}. {{ category.name }}
              </a>
            </div>
          </template>
        </ApolloQuery>
        <!-- END CATEGORIES -->
      </div>
    </div>

    <div class="row">
      <div class="col-12 text-center pt-2">

        <ApolloQuery :query="query" v-if="selectedCategory === 'all'">
          <template slot-scope="{ result: { data, loading }, isLoading }">
            <div v-if="isLoading">Loading...</div>
            <div v-else>
              <div v-for="book of data.books" :key="book.id" class="category">
                {{ book.id }}. {{ book.title }}
              </div>
            </div>
          </template>
        </ApolloQuery>

        <ApolloQuery :query="query" :variables="{ featured: true }" v-else-if="selectedCategory === 'featured'">
          <template slot-scope="{ result: { data, loading }, isLoading }">
            <div v-if="isLoading">Loading...</div>
            <div v-else>
              <div v-for="book of data.booksByFeatured" :key="book.id" class="category">
                {{ book.id }}. {{ book.title }}
              </div>
            </div>
          </template>
        </ApolloQuery>

        <ApolloQuery :query="query" :variables="{ id: selectedCategory }" v-else>
          <template slot-scope="{ result: { data, loading }, isLoading }">
            <div v-if="isLoading">Loading...</div>
            <div v-else>
              <div v-for="book of data.category.books" :key="book.id" class="category">
                {{ book.id }}. {{ book.title }}
              </div>
            </div>
          </template>
        </ApolloQuery>

      </div>
    </div>

  </div>
</template>

<script>
import categoryQuery from '@/graphql/queries/Category.gql'
import categoriesQuery from '@/graphql/queries/Categories.gql'
import booksQuery from '@/graphql/queries/Books.gql'
import booksFeaturedQuery from '@/graphql/queries/BooksFeatured.gql'

export default {
  name: 'Home',
  data() {
    return {
      categoryQuery,
      categoriesQuery,
      booksQuery,
      booksFeaturedQuery,
      selectedCategory: 'all',
      query: booksQuery,
      categories: []
    }
  },
  methods: {
    /**
     * if incoming category matches all -> get all books
     * if incoming category matches featured -> get featured books
     * 
     */
    selectCategory(category) {
      if (category === 'all') {
        this.query = booksQuery
        console.log(category)
      } else if (category === 'featured') {
        this.query = booksFeaturedQuery
        console.log(category)
      } else {
        this.query = categoryQuery
        console.log(category)
      }

      // Set conditional category
      this.selectedCategory = category
      console.log(category)
    }
  }
}
</script>
