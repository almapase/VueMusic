<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>VueMusic</h1>
    <select v-model="selectedCountry" class="" name="">
      <option v-for="country in countries" :value="country.value">
        {{ country.name }}
      </option>
    </select>
    <ul>
      <artist v-for="artist in artists" :artist="artist" :key="artist.mbid"></artist>
    </ul>
  </div>
</template>

<script>
import Artist from './components/Artist.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Chile', value: 'chile'},
        {name: 'España', value: 'spain'},
        {name: 'Colombia', value: 'colombia'},
        {name: 'Mexico', value: 'mexico'},
      ],
      selectedCountry: 'chile'
    }
  },
  components: {
    Artist: Artist
  },
  methods:{
    refreshArtist(){
      const self = this
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.artists = artists
        })
    }
  },
  mounted() {
    this.refreshArtist()
  },
  watch: {
    selectedCountry() {
      this.refreshArtist()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
