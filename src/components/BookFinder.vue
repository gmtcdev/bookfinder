<template>
  <div>Book Finder
    <div class="form">
      <input v-model="searchTerm" placeholder="Search a book">
      <button @click.prevent="search()">Search</button>
    </div>
    <div class="results">
      <div v-for="(result, index) in searchResults" :key="index">
        {{result.volumeInfo.title}},
        <div v-for="(author, index) in result.volumeInfo.authors" :key="index">
          {{author}}
        </div>
        {{result.volumeInfo.publishers}}
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  data() {
    return {
      searchTerm: '',
      searchResults: []
    }
  },
  methods: {
    search() {
      axios.get(`https://www.googleapis.com/books/v1/volumes?q=`+this.searchTerm)
      .then(response => {
        this.searchResults = response.data
        this.searchResults = response.data.items
      })
      .catch(e => {
        console.log(e)
      })
    }
  }
}
</script>

<style>

</style>
