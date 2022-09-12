<template>
    <main>
    <li>
        <img :src="PosterSize + film.poster_path" alt="">
        <h4>Nome film originale:</h4> {{ film.original_title }}
        <h4>Nome film</h4> {{ film.title }}
        <h4>Lingua: 
        <img v-if="film.original_language == 'en'" :src="src('gb')" width="16" height="12">
        <img :src="src(film.original_language)" width="16" height="12">
        </h4>
        <h4>Voto</h4>  {{vote(film.vote_average) }}
        <br>
    </li>
    <li v-for="(serie, i) in series" :key="i">
            <img :src="PosterSize + serie.poster_path" alt="">
            <h4>Nome film originale:</h4> {{ serie.name }}
            <h4>Lingua: 
            <img v-if="serie.original_language == 'en'" :src="src('gb')" width="16" height="12">
            <img :src="src(serie.original_language)" width="16" height="12"></h4>
            <h4>Voto</h4>  {{vote(serie.vote_average) }}
            <br>
    </li>
    </main> 
    
</template>


<script>
export default {
    props: {
       film:{
        type: Object,
        required: true
       },
       serie:{
        type:Object
       }
    },
    data(){
        return{
        PosterSize: 'https://image.tmdb.org/t/p/w342'
        }
    },
    methods:{
        src (el) {
        return  `https://flagcdn.com/16x12/${el.toLowerCase()}.png`;
        },
        vote (num) {
        return Math.round(num /2)
      }
    }
    
}
</script>

<style lang="scss" scoped>

</style>