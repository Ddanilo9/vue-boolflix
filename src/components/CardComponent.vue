<template>
<main>
    <div>
       <img :src="PosterSize + film.poster_path" alt="">
        <h4>Nome film originale:</h4> {{ film.original_title }}
        <h4>Nome film</h4> {{ film.title }}
        <h4>divngua: 
        <img v-if="film.original_language == 'en'" :src="src('gb')" width="16" height="12">
        <img :src="src(film.original_language)" width="16" height="12">
        </h4>
        <span v-for="(voto, index) in vote(film.vote_average)" :key="index">
            <font-awesome-icon icon="fa-solid fa-star" />
        </span>
        <span v-for="(el, index) in vote( 10 - film.vote_average)" :key="index">
            <font-awesome-icon icon="fa-regular fa-star-half" />
        </span>
    
        
        
        
    </div>
    <div v-for="(serie, i) in series" :key="i">
            <img :src="PosterSize + serie.poster_path" alt="">
            <h4>Nome film originale:</h4> {{ serie.name }}
            <h4>divngua: 
            <img v-if="serie.original_language == 'en'" :src="src('gb')" width="16" height="12">
            <img :src="src(serie.original_language)" width="16" height="12"></h4>
            <h4>Voto</h4>  {{vote(serie.vote_average) }}
    </div>   
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
    },
    voteRate(voto){
        return voto
    }
    
}
</script>

<style lang="scss" scoped>

</style>