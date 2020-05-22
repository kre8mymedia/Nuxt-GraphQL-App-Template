<template>
  <div class="container-fluid">
    
    <div class="row">
      <div class="col-12 text-center pt-4">
        <!-- CATEGORIES -->
        <ApolloQuery :query="categoriesQuery">
          <template slot-scope="{ result: { data, loading }, isLoading }">
            <div v-if="isLoading">Loading...</div>
            <div v-else>
              <a href="#" class="category" @click.prevent="selectCategory('all')">All</a> |
              <a href="#" class="category" @click.prevent="selectCategory('featured')">Featured</a> |
              <a
              href="#"
              v-for="category of data.categories"
              :key="category.id"
              @click.prevent="selectCategory(category.id)"
              class="category">
                {{ category.id }}. {{ category.name }}
              </a>
            </div>
          </template>
        </ApolloQuery>
        <!-- END CATEGORIES -->
      </div>
    </div>


    <div class="row">
      <div class="col-12 text-center pt-4">

        <div v-if="selectedCategory === 'all'">
          <ApolloQuery :query="query">
            <template slot-scope="{ result: { data, loading }, isLoading }">
              <div v-if="isLoading">Loading...</div>
              <div v-else>
                <div v-for="book of data.books" :key="book.id" class="book">
                  {{ book.id }}. {{ book.title }}
                </div>
              </div>
            </template>
          </ApolloQuery>
        </div>

        <div v-else-if="selectedCategory === 'featured'">
          <ApolloQuery :query="query" :variables="{ featured: true }">
            <template slot-scope="{ result: { data, loading }, isLoading }">
              <div v-if="isLoading">Loading...</div>
              <div v-else>
                <div v-for="book of data.booksByFeatured" :key="book.id" class="book">
                  {{ book.id }}. {{ book.title }}
                </div>
              </div>
            </template>
          </ApolloQuery>
        </div>

        <div v-else>
          <ApolloQuery :query="query" :variables="{ id: selectedCategory }">
            <template slot-scope="{ result: { data, loading }, isLoading }">
              <div v-if="isLoading">Loading...</div>
              <div v-else>
                <div v-for="book of data.category.books" :key="book.id" class="book">
                  {{ book.id }}. {{ book.title }}
                </div>
              </div>
            </template>
          </ApolloQuery>
        </div>

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
  data() {
    return {
      categoryQuery,
      categoriesQuery,
      booksQuery,
      booksFeaturedQuery,
      selectedCategory: 'all',
      query: booksQuery
    }
  },
  methods: {
    selectCategory(category) {
      if (category === 'all') {
        this.query = booksQuery
      } else if (category === 'featured') {
        this.query = booksFeaturedQuery
      } else {
        this.query = categoryQuery
      }
      
      this.selectedCategory = category
    }
  }
}
</script>