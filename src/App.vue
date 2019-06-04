<template>
  <div id="app">
    <div class="header">
      <div class="feature">
        <img :src="this.feature.url" :alt="this.feature.alt"/>
      </div>
      <div class="search">
        <h1 class="logo">Foto Finder</h1>
        <Search v-on:display-photo="displayPhoto" />
      </div>
    </div>
    <PhotoGallery v-bind:photos="photos"/>
  </div>
</template>

<script>
import Search from './components/Search'
import PhotoGallery from './components/PhotoGallery'
import apiKey from '../apiKey'

export default {
  name: 'App',
  components: {
    Search,
    PhotoGallery
  },
  data () {
    return {
      key: apiKey,
      photos: [],
      feature: ''
    }
  },
  created () {
    this.displayFeature()
  },
  methods: {
    async displayPhoto (photo) {
      const url=`https://api.unsplash.com/search/photos/?page=1&per_page=10&query=${photo.query}&orientation=squarish&client_id=${this.key}`
      try {
        const data = await fetch(url)
        const photos = await data.json()
        this.photos = photos.results
      } catch (error) {
        console.log(error)
      }
    },
    async displayFeature () {
      const url=`https://api.unsplash.com/photos/random?client_id=${this.key}`
      try {
        const data = await fetch(url)
        const photo = await data.json()
        this.feature = { url: photo.urls.small, alt: photo.description }
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #383733;
  min-height: 1600px;
  min-width: 1000px;
  margin: 0px;
  background: #fff
}

.header {
  display: grid;
  grid-template-columns: 400px auto;
  height: 600px;
  box-shadow: 0 3px 5px rgba(0,0,0,0.20)
}

.feature {
  display: flex;
  align-items: center;
  justify-content: center;
}

img {
  height: auto;
  max-width: 400px;
  padding-left: 50px;
}

.search {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-left: 50px;
}

.logo {
  margin: 0px;
  width: 100%;
  font-size: 3rem;
  margin-bottom: 20px;
}

</style>