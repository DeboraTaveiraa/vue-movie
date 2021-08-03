<template>
  <div class="movie-detail" v-if="movie">
    <h2>{{ movie.Title }}</h2>
    <p class="year">{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
    <p>{{ movie.Plot }}</p>
  </div>  
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
  setup () {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
      .then(response => response.json())
      .then(data => {
        movie.value = data;
      })
    });

    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;

  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
    text-align: center;
  }

  .featured-img {
    display: block;
    max-width: 200px;    
    margin: 0 auto 16px auto;
  }

  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;

    &.year {
      text-align: center;
    }
  }
}
</style>