<script>
import axios from 'axios';

  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        places: []
      };
    },
    created: function () {
      this.indexPlaces();
    },
    methods: {
      indexPlaces: function () {
        console.log('places index..')
        axios.get("/places").then(response => {
          console.log(response.data); 
          this.places = response.data
        })
      }
    },
  };
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
   <!-- <h1>{{ places }}</h1> -->
   <div v-for="place in places">
     <p>{{ place.name }}</p>
     <p>{{ place.address }}</p>
     <hr />
  </div>
</div>
</template>

<style></style>