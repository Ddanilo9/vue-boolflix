<template>
  <header>
    <h1 class="logo-title">Boolflix</h1>
    <div class="search-box">
      <h2>Search Movies</h2>
      <input class="text" type="text"  placeholder="search" v-model="queryMovies" />
      <button class="button" @click="fetchMovies()">
       <img :src="search" alt=""></button>  
    </div>
    <div class="search-box">
      <h2>Search Series</h2>
      <input class="text" type="text"  placeholder="search" v-model="querySeries" />
      <button class="button" @click="fetchSeries()">
      <img :src="search" alt=""></button>  
    </div>
  </header>
</template>

<script>
  import axios from "axios";
  import search from '../assets/768px-OOjs_UI_icon_search-ltr.svg.png'
  
  export default {
    data() {
      return {
        api_key: '7f6af0ea9459b62ef9ca7dca6c9afbf9',
        BaseLink: 'https://api.themoviedb.org/3/search',
        BaseLinkSeries: 'https://api.themoviedb.org/3/search/tv?',
        queryMovies: '',
        querySeries: '',
        search: search,
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
            this.queryMovies = ''
          })
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
            this.querySeries = ''
          });
      },
    },
  };
  </script>
 
<style scoped lang="scss">
header{
  display: flex;
  align-items: center;
  padding: 15px 10px;
  background-color: black;
  .logo-title{
    font-size: 35px;
    flex-grow: 1;
  }
  .search-box{
    margin: 0 15px;
    display: flex;
    align-items: center;

    h2{
    font-size: 16px;
    color: white;
    padding: 0 10px;

    }
    .button{
      border: none;
      padding: 5px;
      background-color: rgb(170, 51, 51);
      color: white;
      border-radius: 0 5px 5px 0;
      img{
        width: 13px;
        color: white;
        display: flex;
        align-items: center;
        cursor: pointer;
      }
    }
    .text{
      line-height: 19.5px;
    }

  }
  h1{
    color: rgb(213, 6, 6); 
  }
  
}
</style>
