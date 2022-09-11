<template>
  <div id="app">
    <h1>Search Movies</h1>
    <input type="text"  placeholder="search movies" v-model="queryMovies" />
    <input type="submit" value="search" @click="fetchMovies()" />
    <ul>
      <li v-for="(film, i) in movies" :key="i">
        <h4>Nome film originale:</h4> {{ film.original_title }}
        <h4>Nome film</h4> {{ film.title }}
        <h4>Lingua: 
        <img v-if="film.original_language == 'en'" :src="src('gb')" width="16" height="12">
        <img :src="src(film.original_language)" width="16" height="12">
        </h4>
        <h4>Voto</h4>  {{film.vote_average}}
        <br>
      </li>
    </ul>
    <h1>Search Series</h1>
    <input type="text"  placeholder="search series" v-model="querySeries" />
    <input type="submit" value="search" @click="fetchSeries()" />
    <ul>
      <li v-for="(serie, i) in series" :key="i">
        <h4>Nome film originale:</h4> {{ serie.name }}
        <h4>Lingua: <img :src="src(serie.original_language)" width="16" height="12"></h4>
        <h4>Voto</h4>  {{serie.vote_average}}
        <br>
      </li>
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
        BaseLinkSeries: 'https://api.themoviedb.org/3/search/tv?',
        queryMovies: '',
        querySeries: '',
        movies: [],
        series:[],
      };
    },
    methods: {
      fetchMovies() {
        axios
          .get(
            `${this.BaseLink}/movie?api_key=${this.api_key}&query=${this.queryMovies}`
          )
          .then((res) => {
            console.log(res.data.results)
            this.movies.push(...res.data.results);
          });
      },
      fetchSeries() {
        axios
          .get(
            `${this.BaseLinkSeries}api_key=${this.api_key}&query=${this.querySeries}`
          )
          .then((res) => {
            console.log(res.data.results)
            this.series.push(...res.data.results);
          });
      },
      src (el) {
      return  `https://flagcdn.com/16x12/${el.toLowerCase()}.png`;
      },
    },
  };
  </script>


<style scoped lang="scss">
li{
  padding: 10px;
}
</style>
