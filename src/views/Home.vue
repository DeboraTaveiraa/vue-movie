<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://m.media-amazon.com/images/M/MV5BZmQ5NGFiNWEtMmMyMC00MDdiLTg4YjktOGY5Yzc2MDUxMTE1XkEyXkFqcGdeQXVyNTA4NzY1MzY@._V1_SX300.jpg" alt="Naruto Poster" class="feature-img">
        <div class="detail">
          <h3>Naruto</h3>
          <p>Naruto Uzumaki, a mischievous adolescent ninja, struggles as he searches for recognition and dreams of becoming the Hokage, the village's leader and strongest ninja.</p>
        </div>
      </router-link>      
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="O que você gostaria de pesquisar? (filme, série, game)" v-model="search">
      <p class="not-found" v-if="movies === undefined">Ops! Nenhum resultado encontrado. Tente buscar pelo nome em Inglês!</p>
      <input type="submit" value="Pesquisar">      
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>    
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';

export default {
  setup () {
    const search = ref("");
    const movies = ref([]);   

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          movies.value = data.Search;                    
          search.value = "";          
        })        
      }
    }   

    return {
      search,
      movies,    
      SearchMovies,      
    }
  }
}
</script>

<style lang="scss">
  .home {
    .feature-card {
      position: relative;

      .feature-img {
        display: block;
        width: 100%;
        height: 300px;
        object-fit: cover;

        position: relative;
        z-index: 0;
      }

      .detail {
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0,0,0,0.6);
        padding: 16px;
        z-index: 1;

        h3 {
          color: #FFF;
          margin-bottom: 16px;
        }

        p {
          color: #FFF;
        }
      }
    }

    .search-box {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 16px;      

      input {
        display: block;
        appearance: none;
        border: none;
        outline: none;
        background: none;

        &[type="text"] {
          width: 100%;
          color: #FFF;          
          font-size: 20px;
          padding: 18px 16px;
          border: 1px solid #D7D7D5;
          border-radius: 8px;
          margin-bottom: 15px;
          transition: 0.4s;

          &::placeholder {
            color: #F3F3F3;
          }         
        }

        &[type="submit"] {
          cursor: pointer;
          width: 100%;
          max-width: 300px;
          background-color: #BC4135;
          padding: 16px;
          border-radius: 8px;
          color: #FFF;
          font-size: 20px;
          text-transform: uppercase;
          transition: 0.4s;

          &:active {
            background-color: #5D1A12;
          }
        }
      }

      p {
        color: #D7D7D5;
        margin-bottom: 8px;
      }
    }

    .movies-list {
      display: flex;
      flex-wrap: wrap;
      margin: 0px 0px;

      .movie {        
        max-width: 50%;
        flex: 1 1 50%;
        padding: 16px 8px;

        .movie-link {
          display: flex;
          flex-direction: column;
          height: 100%;

          .product-image {
            position: relative;
            display: block;

            img {
              display: block;
              width: 100%;
              height: 275px;
              object-fit: cover;
            }

            .type {
              position: absolute;
              padding: 8px 16px;
              background-color: #BC4135;
              color: #FFF;
              bottom: 16px;
              left: 0px;
              text-transform: capitalize;
            }
          }

          .detail {
            background-color: #5D1A12;            
            padding: 16px 8px;
            flex: 1 1 100%;
            border-radius: 0px 0px 8px 8px;

            .year {
              color: #D7D7D5;
              font-size: 14px;
            }

            h3 {
              color: #FFF;
              font-weight: 600;
              font-size: 18px;
            }
          }
        }
      }
    }
  }
</style>
