<template>
<main>
    <div class="card">
        <img v-if="film.poster_path !== 'null'" :src="imgSrc(film.poster_path)" alt="">
        <div class="info">
            <h5 class="title"><span>Title: </span>{{ film.title }}</h5> 
            <h5 v-if="film.title != film.original_title"><span>Original Title: </span>{{ film.original_title }}</h5>  
            <span v-for="(voto, index) in vote(film.vote_average)" :key="index">
                <font-awesome-icon icon="fa-solid fa-star" />
            </span>
            <span v-for="(el, index) in vote(10 - film.vote_average)" :key="index">
                <font-awesome-icon icon="fa-regular fa-star" />
            </span>
            <p><span>Overview: </span>{{film.overview}}</p>
            <h4>Lang: 
                <img v-if="film.original_language == 'en'" :src="src('gb')" width="16" height="12">
                <img :src="src(film.original_language)" width="16" height="12">
            </h4>
        </div>
    </div>
    <div v-for="serie in series" :key="serie.id">
            <img :src="PosterSize + serie.poster_path" alt="">
            <h4>Nome film originale:</h4> {{ serie.name }}
            <h4>lingua: 
            <img v-if="serie.original_language == 'en'" :src="src('gb')" width="16" height="12">
            <img :src="src(serie.original_language)" width="16" height="12"></h4>
            <span v-for="(voto, index) in vote(serie.vote_average)" :key="index">
            <font-awesome-icon icon="fa-solid fa-star" />
        </span>
        <span v-for="(el, index) in vote( 10 - serie.vote_average)" :key="index">
            <font-awesome-icon icon="fa-regular fa-star" />
        </span>
            
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
        PosterSize: 'https://image.tmdb.org/t/p/w342',
        foto: 'https://picsum.photos/200/300'
        }
    },
    methods:{
        src (el) {
        return  `https://flagcdn.com/16x12/${el.toLowerCase()}.png`;
        },
        vote (num) {
        return Math.round(num /2)
        },
        imgSrc(el){
            return this.PosterSize+el
        }
    },
    
}
</script>

<style lang="scss" scoped>
.card{
position: relative;
    .info{
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    background-color: black;
    color: white;
    padding: 11px 15px;
    overflow: auto;
    display: none;
    h5{
        font-weight: 500;
        span{
            font-size: 16px;
            font-weight: 800;
        }
    }    
    }
}


</style>