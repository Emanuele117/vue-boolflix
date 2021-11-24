<template>
  <div class="container movieAndSeries">
    <SiteHeader @search-tvshows="search" />
    <h1 class="results-films">Results for Movies:</h1>
    <div class="container movies">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <div class="img">
          <img
            :src="`https://image.tmdb.org/t/p/w200/${movie.poster_path}`"
            alt=""
          />
        </div>
        <div class="info">
          <h5>Titolo: {{ movie.title }}</h5>
          <h5>Titolo Originale: {{ movie.original_title }}</h5>
          <h5>Voto: {{ movie.vote_average }}</h5>
          <h5>Overview: {{ movie.overview }}</h5>
          <img
            :src="
              require(`../assets/img-bandiere/${movie.original_language}.png`)
            "
            alt=""
          />
        </div>
      </div>
    </div>
    <h1 class="results-serieTv">Results for Series:</h1>
    <div class="container series">
      <div class="serieTv" v-for="serie in series" :key="serie.id">
        <div class="img_series">
          <img
            :src="`https://image.tmdb.org/t/p/w200/${serie.poster_path}`"
            alt=""
          />
        </div>
        <div class="info_series">
          <h5>Titolo: {{ serie.name }}</h5>
          <h5>Titolo Originale: {{ serie.original_name }}</h5>
          <h5>Voto: {{ serie.vote_average }}</h5>
          <h5>Overview: {{ serie.overview }}</h5>
          <img
            :src="
              require(`../assets/img-bandiere/${serie.original_language}.png`)
            "
            alt=""
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SiteHeader from "./SiteHeader.vue";
import axios from "axios";

export default {
  data() {
    return {
      searchString: "",
      movies: [],
      series: [],
      movies_url: "https://api.themoviedb.org/3/search/movie",
      series_url: "https://api.themoviedb.org/3/search/tv",
      api_key: "2f8b947658c764e57b4f430bb9ca5991",
    };
  },
  methods: {
    search(searchString) {
      const full_url = `${this.movies_url}?api_key=${this.api_key}&query=${searchString}`;
      const series_url = `${this.series_url}?api_key=${this.api_key}&query=${searchString}`;

      axios
        .get(full_url)
        .then((r) => {
          console.log(r.data);
          this.movies = r.data.results;
        })
        .catch((e) => {
          console.log(e, "OPS");
        });

      axios
        .get(series_url)
        .then((r) => {
          console.log(r.data);
          this.series = r.data.results;
        })
        .catch((e) => {
          console.log(e, "OPS");
        });
    },
  },
  components: {
    SiteHeader,
  },
};
</script>

<style lang="scss">
#app {
  background-color: black;
}
.results-films {
  color: white;
  font-size: 22px;
  margin-bottom: 2rem;
  margin-top: 5rem;
  margin-left: 3rem;
}
.movies {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  .movie {
    position: relative;
    margin-bottom: 1rem;
  }
  .movie:hover {
    .info {
      display: block;
    }
  }

  .info {
    padding: 15px;
    background-color: rgba($color: #000000, $alpha: 0.9);
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;

    h5 {
      font-size: 10px;
      color: white;
    }
  }
}
.results-serieTv {
  color: white;
  font-size: 22px;
  margin-bottom: 2rem;
  margin-top: 2rem;
  margin-left: 3rem;
}
.series {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  .serieTv {
    position: relative;
    margin-bottom: 1rem;
  }
  .serieTv:hover {
    .info_series {
      display: block;
    }
  }
  .info_series {
    padding: 20px;
    background-color: rgba($color: #000000, $alpha: 0.9);
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;

    h5 {
      font-size: 9px;
      color: white;
    }
  }
}
</style>