<template>
  <div class="search">
    <h2>Search For Delicious Meal!</h2>
    <form v-on:submit.prevent="getResult(query)">
      <input class="cari" type="text" placeholder="Search..." v-model="query">
    </form>
    <div class="results" v-if="results">

      <div v-for="result in results">
        <br><img class="gambar" v-bind:src="result.strMealThumb" />
        <h1 v-bind:title="result.strMeal"></h1>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult (query) {
      axios.get('https://www.themealdb.com/api/json/v1/1/search.php?s=' + query).then(response => {
        console.log(response.data.meals)
        this.results = response.data.meals
      })
    }
  }
}
</script>

<style scoped>
.result img {
  height: 300px;
  margin: 10px;
}

.gambar {
  width: 400px;
  box-shadow: 0 15px 25px 0 rgb(197, 176, 197);
  border-radius: 50px;
}

h1, h2 {
  font-weight: normal;
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

.cari {
  width: 300px;
  height: 40px;
  border-radius: 100px;
  border-color: darkmagenta;
  
}
</style>