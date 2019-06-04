<template>
  <form @submit="searchPhotos" class="search-form">
    <input type="text" v-model="query" name="query" placeholder="Search for photos . . ." class="search-input">
    <input type="submit" value='' class="submit-btn">
  </form>
</template>

<script>

export default {
  name: 'Search',
  data () {
    return {
      query: ''
    }
  },
  methods: {
    searchPhotos (e) {
      e.preventDefault()
      const photo = {
        id: 1,
        query: this.query
      }
      this.$emit('display-photo', photo)
    }
  }
}
</script>

<style scoped>

.search-input {
  height: 50px;
  width: 80%;
  border: none;
  border-bottom: solid #b3ab9b 2px;
  box-sizing: border-box;
  color: #40403d;
  padding-left: 5px;
  font-size: 1rem;
}

.search-input:focus {
  outline: none;
}

.submit-btn {
  border: none;
}

.submit-btn:focus {
  outline: none;
}

</style>