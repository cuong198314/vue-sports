<template>
  <div class="Search">
    <h1>This is the search page</h1>
    <h2>Please enter your search query!</h2>
    <label>Query:
      <input type="text" id="Query" v-model="message">
    </label>
    <h2>Your search results:</h2>
   
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      message: ''
    }
  }
 
}
</script>