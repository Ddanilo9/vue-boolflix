<template>
  <header>
    <h1>Boolflix</h1>
    <h2>Search Movies</h2>
    <input type="text"  placeholder="search movies" v-model="queryMovies" />
    <input type="submit" value="search" @click="fetchMovies()" />
    <h2>Search Series</h2>
    <input type="text"  placeholder="search series" v-model="querySeries" />
    <input type="submit" value="search" @click="fetchSeries()" />
  </header>
</template>

<script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        api_key: '7f6af0ea9459b62ef9ca7dca6c9afbf9',
        BaseLink: 'https://api.themoviedb.org/3/search',
        BaseLinkSeries: 'https://api.themoviedb.org/3/search/tv?',
        queryMovies: '',
        querySeries: '',
        movies: [],
        series:[],
      };
    },
    methods: {
      fetchMovies() {
        if (this.queryMovies.trim() === '')
        return
        axios
          .get(
            `${this.BaseLink}/movie?api_key=${this.api_key}&query=${this.queryMovies}`
          )
          .then((res) => {
            console.log(res.data.results)
            // this.movies = res.data.results;
            this.$emit('onSearch', res.data.results)
          });
      },
      fetchSeries() {
        if (this.querySeries.trim() === '')
        return
        axios
          .get(
            `${this.BaseLinkSeries}api_key=${this.api_key}&query=${this.querySeries}`
          )
          .then((res) => {
            console.log(res.data.results)
            this.$emit('onSearch', res.data.results);
          });
      },
    },
  };
  </script>
 

<style scoped lang="scss">
header{
  display: flex;
  align-items: center;
  padding: 10px 5px;
  background-color: black;
  h1{
    color: red;
  }
  h2{
    color: white;
    padding: 0 20px;
  }
}
</style>
