<template>
<h1>
    <b>{{movieVideo.title}}</b>

</h1>
<p>
    <b>Index: {{movieVideo.id}}</b><br> <b>Popularity: {{movieVideo.popularity}}</b>  
</p>
<a :href="'https://www.youtube.com/watch?v='+ 
    infoVideo.key" target="_blank"><b>TRAILER</b></a> 
</template>

<script>

export default{
    name: "MovieVideo",
    props:['movieVideo'],
    data(){
        return{
            urlyoutube: '',
            infoVideo: []
        }
    },
    methods:{
        findVideo: function(idVideo){
        let url=''.concat('https://api.themoviedb.org/3/movie/', idVideo, 
        '/videos?api_key=d9013d40a0e8752e4d5f46b12c137b91&language=en-US');
        fetch(url)
        .then(result=>result.json())
        .then((data)=>{
          let firstData= data['results'];
          this.infoVideo= firstData[0];
          console.log( 'DATAVIDEOS:', this.dataVideo);
          });
    
      }
    },
    created() {
        this.findVideo(this.movieVideo.id);
    },


}

</script>

<style scoped>
h1{
    -webkit-text-stroke: 1px var(--focuspeli);
}
a{ 
    background-color: var(--body);
    color: #f1f4ff;
    padding: 1.2rem;
    position: absolute;
    bottom: 0;
    right: 0;
    left: 0;
    text-align: center;
}

a:hover{
   color: var(--body); 
}
p{
    color: white;
    -webkit-text-stroke: 0.4px black;
    font-size: 1.5rem;
}
</style>
