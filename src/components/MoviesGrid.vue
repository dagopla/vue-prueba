<template>
<!-- se renderiza los detalles de la pelicula si es llamada  -->
<div v-if="rend" class="focusPeli">
    <div class="focusimg"><MoviePart :moviePart= "focusPeli"/></div>
    <div class="focusDetails"><MovieVideo :movieVideo="focusPeli" /><p>Fechas: {{focusPeli.release_date}} <br>{{focusPeli.overview}} </p></div>
</div>
<!-- Lista de peliculas buscadas -->
<ul>
    <li v-for="peli in moviesList" :key="peli.id"  @click="focusMovie(peli)">
        <div class="details-peli"><MovieVideo :movieVideo="peli" /></div>
        <div class="img-div"><MoviePart :moviePart= "peli"/></div>
        </li>  
</ul>

</template>

<script>
import MoviePart from './MoviePart.vue'
import MovieVideo from './MovieVideo.vue'

export default {
    components: { MoviePart, MovieVideo },
    name: 'MoviesGrid',
    props:['moviesList'],
    data(){
        return{
            rend:false,
            focusPeli:[]
        }
    },
    methods:{
        focusMovie: function(peli){
            this.rend=true;
            this.focusPeli=peli;
            scrollTo(0,0);
            console.log( peli)
        }
    }
   
}
</script>

<style  scoped>
@import '@/assets/MoviesGridStyle.css';

</style>

