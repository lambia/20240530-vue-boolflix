<script>
import AppHeader from './components/AppHeader.vue';
import axios from 'axios';

export default {
  name: "App",
  components: {
    AppHeader
  },
  data() {
    return {
      apiMoviesUrl: "https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=la+vita+è+bella",
      movies: [],
      imagePrefix: "https://image.tmdb.org/t/p/w780",
      bandiere: {
        it: "https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/1200px-Flag_of_Italy.svg.png",
        en: "https://upload.wikimedia.org/wikipedia/commons/a/a5/Flag_of_the_United_Kingdom_%281-2%29.svg",
      }
    }
  },
  methods: {
    getImageUrl(imagePath) {
      return this.imagePrefix + imagePath;
    },
    getVote(vote) {
      let newVote = vote / 2;
      newVote = newVote.toFixed(2);
      newVote = Math.round(newVote);
      return newVote;
    },
    getStars(vote, numeroStella) {
      let newVote = this.getVote(vote)

      let classe = 'fa-regular fa-star';

      if (newVote >= numeroStella) {
        classe = 'fa fa-star';
      }

      return classe;
    },
    getFlag(language) {

      let result = false;

      if (language == "it") {
        result = "https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/1200px-Flag_of_Italy.svg.png";
      } else if (language == "en") {
        result = "https://upload.wikimedia.org/wikipedia/commons/a/a5/Flag_of_the_United_Kingdom_%281-2%29.svg";
      }

      return result;
    }
  },
  mounted() {
    console.log("App montata");

    axios.get(this.apiMoviesUrl).then(r => {
      console.log(`Chiamata completata: ${r.status}`);
      console.log("La chiamata ha restituito: ", r.data.results);
      this.movies = r.data.results;
    }).catch(error => {
      console.log("Ops, qualcosa è andato storto!");
    });
  }
}
</script>

<template>
  <AppHeader />
  <h2>Film: </h2>
  <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quia, illo!</p>

  <h2>Serie: </h2>
  <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Expedita, repellat?</p>

  <div class="card" v-for="film in movies">
    <p>{{ film.title }}</p>
    <img class="poster" :src="imagePrefix + film.poster_path" />
    <!-- <img class="poster" :src="getImageUrl(film.poster_path)" /> -->

    <!-- <p>{{ (film.vote_average / 2).toFixed(2) }}</p> -->
    <p>Voto: {{ getVote(film.vote_average) }}</p>
    <p>
      <i :class="getStars(film.vote_average, 1)"></i>
      <i :class="getStars(film.vote_average, 2)"></i>
      <i :class="getStars(film.vote_average, 3)"></i>
      <i :class="getStars(film.vote_average, 4)"></i>
      <i :class="getStars(film.vote_average, 5)"></i>
    </p>

    <img v-if="getFlag(film.original_language)" class="flag" :src="getFlag(film.original_language)" />
    <p v-else>{{ film.original_language }}</p>

  </div>

</template>

<style>
.card {
  margin-bottom: 1rem;
}

.card .poster {
  width: 6rem;
}

.flag {
  width: 1.5rem;
}
</style>