<template>
    <div class='gallery-container'>
      <div v-bind:key="photo.id" v-for="photo in photos" class="image">
        <img :src="photo.urls.small" :alt="photo.alt_description" />
        <p>Photo by {{photo.user.name}}</p>
      </div>
    </div>
</template>

<script>
export default {
  name: 'PhotoGallery',
  props: ['photos']
}
</script>

<style scoped>
p {
  font-weight: normal;
  color: #40403d;
}

.gallery-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.image {
  background-color: #fff;
  height: 300;
  width: 400px;
  border: solid #F8F8FF 5px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  margin: 10px;
  box-shadow: 0 3px 5px rgba(0,0,0,0.20)
}
</style>