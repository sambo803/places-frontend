<script>
import axios from 'axios';

  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        places: [],
        newPlaceParams: {}, 
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
      },
      createPlace: function () {
        axios.post("/places", this.newPlaceParams).then((response) => {
          console.log("places create", response);
          this.places.push(response.data);
          this.newPlaceParams = {};
        })
        .catch((error) => {
          console.log("places create error", error.response);
        });
      }
    },
  };
</script>


<template>
  <div class="home">
    <h1>{{ message }}</h1>
      <h1>New Place</h1>
      <div>
      Name:
      <input type="text" v-model="newPlaceParams.name" />
      Address:
      <input type="text" v-model="newPlaceParams.address" />
      image_url:
      <input type="text" v-model="newPlaceParams.url" />
     <p> <button v-on:click="createPlace()">Create Place</button></p>
      </div>
   <!-- <h1>{{ places }}</h1> -->
   <h1>All Places</h1>
   <div v-for="place in places">
     <p>{{ place.name }}</p>
     <p>{{ place.address }}</p>
     <p>{{ place.image_url }}</p>
     <br/>
     <!-- <button v-on:click="createPlace">Create New Place</button> -->
  </div>
</div>
</template>

<style></style>