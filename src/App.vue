<script>
import MoviesGrid from "./components/MoviesGrid.vue"
import MoviesId from "./components/MoviesId.vue"

export default{
  name:'App',
  components:{
    MoviesGrid, MoviesId
  },
  data(){
    return{
      user: [],
      find:'',
      details:[],
      render:true,
      dataVideos:[],

    }
},
methods:{
// La funcion trae de la base de datos las peliculas con los caracteres similares introducidos
// en la barra de busqueda
  runSearch: function(keyword) {
    let url='';
    //Datos con las palabras claves
    if (isNaN(keyword)){
      url=''.concat('https://api.themoviedb.org/3/search/movie?api_key=d9013d40a0e8752e4d5f46b12c137b91&language=en-US',
      '&query=', keyword, '&page=1&include_adult=false');
      this.searchData(url);
      
    //Datos con la ID de la pelicula
    }else{
      url=''.concat('https://api.themoviedb.org/3/movie/', keyword, '?api_key=d9013d40a0e8752e4d5f46b12c137b91&language=en-US');
      this.findVideo(keyword);
      this.searchData(url);
    }
  },
  // Funcion para obtener las key de los videos para cada id
  findVideo: function(idVideo){
    let url=''.concat('https://api.themoviedb.org/3/movie/', idVideo, 
    '/videos?api_key=d9013d40a0e8752e4d5f46b12c137b91&language=en-US');
    fetch(url)
    .then(result=>result.json())
    .then((data)=>{
      let firstData= data['results'];
      this.dataVideos= firstData[0];
      console.log( 'DATAVIDEOS:', this.dataVideos);
      });
    
  },
  //Funcion que busca en la base de datos
  searchData: function(url){
    fetch(url)
    .then(result=>result.json())
    .then((data)=>{
      this.details=data['results'];
      // Si la entrada es una ID se guardan los datos sin la columna results
      if(this.details==undefined){
        this.details=data;
        this.render=false;
      }
      console.log('di:', this.details);
      //para cada pelicula se halla el video en youtube

    });
  },
},
// Muestra peliculas aleatorias al cargar la pagina.
mounted(){
  document.addEventListener('DOMContentLoaded', this.runSearch("aeioubcdfghjklmnwqps"[Math.floor(Math.random() * 20)]));
}

}


</script>

<template>
<!-- Encabezado de la pagina -->
  <header>
    <a href="../index.html"><h1 class="title-head"> <b>Movies Search</b></h1></a>
    <div class="div-input">
      <input aria-label="Search" placeholder="Ex: Spiderman or 634649" type="search" v-model="find" @keyup.enter="runSearch(find)">
      <button v-on:click="runSearch(find)" class="button-S">🔍</button>
    </div>

  </header>
  <!-- Los componentes de la app, dependiendo de la entrada se renderiza uno u otro -->
  <MoviesGrid :moviesList="details" v-if="render" />
  <MoviesId :moviesList="details" :dataVideo="dataVideos" v-else />
 


</template>

<style>
@import './assets/base.css';

</style>
