<template>
  <div id="app">
    <MainHeader @onSearch="setMovies"/>
    <div  class="container grid">
      <CardComponent 
      v-for="film in movies" :key="film.id" :film="film"></CardComponent>
    </div>
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
        queryMovies: '',
        movies: [],
    }
  },
  methods: {
    setMovies(movies, series) {
      this.movies = movies
      this.series = series
    }
  },
}
</script>

<style lang="scss">
@import './style/general.scss';
.container{
    max-width: 1300px;
    margin: 0 auto;
    margin-top: 30px;
}
.grid{
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-column-gap: 10px;
    grid-row-gap: 10px;
}

</style>
