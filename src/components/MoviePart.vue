<template>
<img :src= "'http://image.tmdb.org/t/p/w300'+ moviePart.poster_path"
 :alt= "moviePart.title" width="230" height="345">

</template>

<script>

export default {
    name: 'MoviePart',
    props: ['moviePart'],
    
}

</script>

<style scoped>

img{
    border-radius: var(--borde-img);
    background-color: azure;
    box-shadow: 0 0 3rem #000; 
}

</style>