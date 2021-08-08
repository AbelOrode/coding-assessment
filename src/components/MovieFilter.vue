<template>
  <div class="exercise-header">
    <h2>Exercise 2 - Filterable content</h2>
  </div>
  <div class="grid-container">

    <div class="grid-item">
      <select id="filterGenre">
        <option v-for="movie in movies" :key="movie.title" :value="movie.genre[counter++]">{{ movie.genre[0] }}</option>
      </select>
    </div>

    <div class="grid-item">
      <select id="filterYear">
        <option v-for="movie in movies" :value="movie.year" :key="movie.year">{{ movie.year }}</option>
      </select>
    </div>

    <div class="grid-item">
      <input class="text" v-model="searchTerm" id="searchBar" placeholder="Search movie by title">
    </div>
  </div>

  <div class="grid-item">
    <input type="radio" name="media_type" id="movie" value="movie" checked>
    <label for="movie">Movie</label>&nbsp; &nbsp;
    <input type="radio" name="media_type" id="book" value="book">
    <label for="book">Book</label>
  </div>

  <div class="content">
    <div class="grid-container">
      <div class="grid-item" v-for="(movie, title) in filterSearch" :key="title">
        <img :src="movie.poster" class="responsive">
        <p class="movie-title"><span>{{ movie.title }} &nbsp;{{ movie.year }}</span></p>
        <p class="movie-title"><span>Genre{{ movie.genre }} </span></p>
      </div>
    </div>
  </div>
</template>

<script>
import movieData from "../data.json"

export default {


  data() {
    return {
      movies: movieData.media,
      counter: 0,
      searchTerm: '',
      movieYear: null,

    }
  },

  computed: {
    filterSearch() {

        return this.movies.filter(movie => {
          return movie.title.toLowerCase().match(this.searchTerm.toLowerCase())
        })
    }

  },
  methods: {
    handleChange(event) {
      if (event.target.options.selectedIndex > -1) {
        let selectedOption = event.target.options.selectedIndex;
        console.log(event.target.options[selectedOption].text);
        return this.movies.filter(movie => {
          movie.year.match(event.target.options[selectedOption].text)
        })
      }

    },
    changeMovieYear(event) {
      this.movies.year = event.target.value
      this.selectMovieYear = event.target.options[event.target.options.selectedIndex].text

    }
  }
}
</script>

<style>

</style>