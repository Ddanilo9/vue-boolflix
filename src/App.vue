<template>
  <div id="app">
    <MainHeader @onSearch="setMovies"/>
    <ul>
      <CardComponent 
      v-for="(film, i) in movies" :key="i" :film="film"></CardComponent>
    </ul>
    
  </div>
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import CardComponent from './components/CardComponent.vue'


export default {
  name: 'App',
  components: {
    MainHeader,
    CardComponent,
  },
  data() {
    return{
      api_key: '7f6af0ea9459b62ef9ca7dca6c9afbf9',
        BaseLink: 'https://api.themoviedb.org/3/search',
        // BaseLinkSeries: 'https://api.themoviedb.org/3/search/tv?',
        queryMovies: '',
        // querySeries: '',
        movies: [],
        // series:[],
        // PosterSize: 'https://image.tmdb.org/t/p/w342'
    }
  },
  methods: {
    setMovies(movies, series) {
      this.movies = movies
      this.series = series
    }
  }
}
</script>

<style lang="scss">
@import './style/general.scss'
</style>
