<template>
  <div id="app">
    <input type="text"  placeholder="search movies" v-model="query" />
    <input type="submit" value="search" @click="fetch()" />
    <ul>
      <li v-for="(film, i) in movies" :key="i">
        {{ film.original_title }}
        {{ film.title }}
        {{ film.original_language }}
      </li><br>
    </ul>
  </div>
</template>

<script>
  import axios from "axios";
  
  export default {
    name: "App",
    components: {},
    data() {
      return {
        api_key: '7f6af0ea9459b62ef9ca7dca6c9afbf9',
        BaseLink: 'https://api.themoviedb.org/3/search',
        query: '',
        movies: [],
      };
    },
    methods: {
      fetch() {
        axios
          .get(
            `${this.BaseLink}/movie?api_key=${this.api_key}&language=it_IT&query=${this.query}`
          )
          .then((res) => {
            console.log(res.data.results)
            this.movies.push(...res.data.results);
          });
      },
    },
  };
  </script>


<style scoped lang="scss">

</style>
