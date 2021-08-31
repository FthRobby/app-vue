<template>
    <div class="mt-4 mx-4">
      <div class="home">

        <!-- Thumbnail beranda -->
        <div class="featured-card">
          <router-link to="/movie/tt0114709">
            <!--<img src="https://m.media-amazon.com/images/M/MV5BZmQ5NGFiNWEtMmMyMC00MDdiLTg4YjktOGY5Yzc2MDUxMTE1XkEyXkFqcGdeQXVyNTA4NzY1MzY@._V1_SX300.jp" alt="Naturo Poster" class="featured-img"/>-->
            <img src="https://p4.wallpaperbetter.com/wallpaper/697/872/835/movie-toy-story-4-bo-peep-buzz-lightyear-woody-toy-story-hd-wallpaper-preview.jpg" alt="ToyStory Poster" class="featured-img img-fluid"/>
            <div class="detail">
              <h3>Toy Story</h3>
              <p>A little boy named Andy loves to be in his room, playing with his toys, especially his doll named "Woody".</p>
            </div>
          </router-link>
        </div><br>

        <form @submit.prevent="SearchMovies()" class="search-box">
          <input type="text" placeholder="Cari film " v-model="search"/>
          <input type="submit" value="Cari">
        </form><br>

        <div class="movies-list">
          <div class="movie" v-for="movie in movies" :key="movie.imdbID">
            <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
              <div class="product-image">
                <img :src="movie.Poster" alt="Movie Poster" />
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
    </div>
</template>


<script>
import {ref} from 'vue';
import env from '@/env.js'

export default {
  setup() {
    const search = ref ("");
    const movies = ref ([]);

    const SearchMovies = () => {
      if (search.value != "") {
       fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
       .then(response => response.json())
       .then(data => {
         movies.value = data.Search;
         search.value = "";
       });
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
* {
  text-decoration: none !important;
    
}
.home {
  

  .featured-card {
    position: relative ;

    .featured-img {
      display: block !important;
      width: 100% !important;
      height: 500px !important;
      object-fit: cover !important;

      position: relative !important;
      z-index: 0 !important;
    }

    .detail {
      position: absolute !important;
      left: 0 !important;
      right: 0 !important;
      bottom: 0 !important;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px !important;
      z-index: 1 !important;

      h3 {
        color: #FFF !important;
        margin-bottom: 16px !important;
      }

      p {
        color: #FFF !important;
      }
    }
  }

  .search-box {
    display: flex !important;
    flex-direction: column !important;
    justify-content: center !important;
    padding: 16px !important;
    align-items: center !important;

    input {
      display: block ;
      appearance: none ;
      border: none ;
      outline: none ;
      background: none;

      &[type="text"] {
        width: 100% !important;
        color: #FFF !important;
        background-color: #496583 !important;
        font-size: 20px !important;
        padding: 10px 16px !important;
        border-radius: 8px !important;
        margin-bottom: 15px !important;
        transition: 0.4s !important;

        &::placeholder {
          color: #f3f3f3 !important;
        }

        &focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100% !important;
        max-width: 300px !important;
        background-color: #42B883 !important;
        padding: 16px !important;
        border-radius: 8px !important;
        color: #FFF !important;
        font-size: 20px !important;
        text-transform: uppercase !important;
        transition: 0.4s !important;

        &:active {
          background-color: #3B8070 !important;
        }
      }
    }
  }

  .movies-list {
    display: flex !important;
    flex-wrap: wrap !important;
    margin: 0px 8px !important;


    .movie {
      max-width: 50% !important;
      flex: 1 1 50% !important;
      padding: 16px 8px !important;

      .movie-link {
        display: flex !important;
        flex-direction: column !important;
        height: 100% !important;

        .product-image {
          position: relative !important;
          display: block !important;

          img {
            display: block !important;
            width: 100% !important;
            height: 275px !important;
            object-fit: cover !important;
          }

          .type {
            position: absolute !important;
            padding: 8px 16px !important;
            background-color: #42B883 !important;
            color: #FFF !important;
            bottom: 16px !important;
            left: 0px !important;
            text-transform: capitalize !important;
          }
        }

        .detail {
          background-color: #496583 !important;
          padding: 16px 8px !important;
          flex : 1 1 100% !important;
          border-radius: 0px 0px 8px 8px !important;

          .year {
            color: #AAA !important;
            font-size: 14px !important;
          }

          h3 {
            color: #FFF !important;
            font-weight: 600 !important;
            font-size: 18px !important;
          }
        }
      }
    }
  }
}
</style>