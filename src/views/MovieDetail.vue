<template>
  <div class="movie-detail">
    <div class="container">
      <h2 class="text-white">{{ movie.Title }}</h2>
      <p class="text-white">{{ movie.Year }}</p>
      <hr class="bg-white">
        <div class="container"><img :src="movie.Poster" alt="Movie Poster" class="featured-img " /></div>
      <hr class="bg-white">  
      <br><br>
      <h3 class="text-white">About Movie :</h3>
      <p class="title-movie text-white">{{ movie.Plot }}</p>

      <button type="button" class="btn text-white">Watch Movie</button>
    </div>

  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
      .then(response => response.json())
      .then(data => {
        movie.value = data;
      });
    });

    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail{
  padding: 16px;
  width: 50px;
  min-width: 100%;
  box-sizing: border-box;
  background-color: darkcyan;

  h2 {

    font-size: 35px ;
    font-weight: 700 ;
    margin-bottom: 16px ;
    font-family: 'Roboto', sans-serif;
    text-transform: uppercase;
  }

  h3 {
    font-size: 30px;
    font-family: 'Quicksand', sans-serif;
  }

  .title-movie {
    font-family: 'Quicksand', sans-serif;

  }

  .fetured-img {
    display: block !important;
    max-width: 200px !important;
    margin-block: 16px !important;
  }

  .btn {
    background-color: #2C3D4E;

    
  }

}
</style>
<style>
 @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap');
 @import url('https://fonts.googleapis.com/css2?family=Arvo&display=swap');
 @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@500&display=swap');
</style>