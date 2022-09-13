<template>
<main>
    <div class="card">
        <img :src="getPath(film.poster_path)" alt="">
        <div class="info">
            <h4 class="title"><span>Title: </span>{{ film.title }}</h4> 
            <h4 class="original-t"
             v-if="film.title != film.original_title"><span>Original Title: </span>{{ film.original_title }}</h4>  
            <span class="vote" v-for="(voto, index) in vote(film.vote_average)" :key="index" style="color: gold">
                <font-awesome-icon icon="fa-solid fa-star" />
            </span>
            <span class="vote" v-for="(el, index) in vote(10 - film.vote_average)" :key="index">
                <font-awesome-icon icon="fa-regular fa-star" />
            </span>
            <p><span>Overview: </span>{{film.overview}}</p>
            <h4><span>Lang: </span>  
                <img v-if="film.original_language === 'en'" :src="src('gb')" width="16" height="12">
                <img v-else :src="src(film.original_language)" width="16" height="12">
            </h4>
        </div>
    </div>
    <div class="card" v-for="serie in series" :key="serie.id">
        <img :src="getPath(serie.poster_path)" alt="">
        <div class="info">
            <h4 class="title"><span>Title: </span>{{ serie.title }}</h4> 
            <h4 class="original-t"
             v-if="serie.title != serie.original_title"><span>Original Title: </span>{{ serie.original_title }}</h4>  
            <span class="vote" v-for="(voto, index) in vote(serie.vote_average)" :key="index" style="color: gold">
                <font-awesome-icon icon="fa-solid fa-star" />
            </span>
            <span class="vote" v-for="(el, index) in vote(10 - serie.vote_average)" :key="index">
                <font-awesome-icon icon="fa-regular fa-star" />
            </span>
            <p><span>Overview: </span>{{serie.overview}}</p>
            <h4><span>Lang: </span>  
                <img v-if="serie.original_language === 'en'" :src="src('gb')" width="16" height="12">
                <img v-else :src="src(serie.original_language)" width="16" height="12">
            </h4>
        </div>
            
    </div>   
</main> 

</template>


<script>
import foto from '../assets/netflix-1200x900.jpg'

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
        foto: foto
        }
    },
    methods:{
        src (el) {
        return  `https://flagcdn.com/16x12/${el.toLowerCase()}.png`;
        },
        vote (num) {
        return Math.round(num /2)
        },
        getPath(el){
            if(el == null){
                return this.foto
            }
            return this.PosterSize + el 
        }
    },
    
}
</script>

<style lang="scss" scoped>
    img{
        box-shadow: rgba(6, 24, 44, 0.4) 0px 0px 0px 2px, rgba(6, 24, 44, 0.65) 0px 4px 6px -1px, rgba(255, 255, 255, 0.08) 0px 1px 0px inset;
    }
.card{
position: relative;
height: 100%;
cursor: pointer;
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
    opacity: 0;
    border: 1px solid white;
    transition: opacity 0.8s;
    &::-webkit-scrollbar {
    display: none;}
    &:hover{
        opacity: 1;
    }
    .title, .original-t, .vote{
        margin-bottom: 3px;
    }
    h4, p{
        font-weight: 500;
        font-size: 14px;
        color: rgb(161, 151, 151);
        
        span{
            font-size: 16px;
            font-weight: 800;
            color: rgb(255, 255, 255);
        }
    }
    p{
        span{
            font-size: 16px;
            font-weight: 800;
            color: rgb(255, 255, 255);
        }
    }    
    }
}


</style>