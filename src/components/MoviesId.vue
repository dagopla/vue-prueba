<template>
<div class="content">
<ul>
    <li :key="moviesList.id" >
        <div class="img-div" ><MoviePart :moviePart= "moviesList"/></div>
    </li>
</ul>
<div class="info_peli">
    <h1>{{moviesList.title}}</h1>
    <h2><b>Popularity: </b>{{moviesList.popularity}}</h2>
    <h2><b>ID: </b>{{moviesList.id}}</h2>
    <h3>{{moviesList.release_date}}</h3>
    <p>{{moviesList.overview}}</p> <br>
    <a :href="'https://www.youtube.com/watch?v='+ 
    dataVideo.key" target="_blank"><b>TRAILER</b></a> 
</div>
</div>
</template>

<script>
import MoviePart from './MoviePart.vue'
import MovieVideo from './MovieVideo.vue'

export default {
    components: { MoviePart, MovieVideo},
    name: 'MoviesId',
    props:['moviesList', 'dataVideo'],
  

}
</script>

<style  scoped>
@import '@/assets/MoviesIdStyle.css';
</style>
