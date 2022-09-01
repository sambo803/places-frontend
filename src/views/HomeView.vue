<script>
import axios from 'axios';

  export default {
    data: function () {
      return {
        message: "Welcome to Places!!",
        places: [],
        newPlaceParams: {}, 
        currentPlace: {},
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
      },
      showPlace: function (place) {
        this.currentPlace = place;
        document.querySelector("place-details").showModal();
      }
    },
  };
</script>


<template>
  <div class="home">
      <h3>New Place:</h3>
      <div>
      Name:
      <input type="text" v-model="newPlaceParams.name" />
      Address:
      <input type="text" v-model="newPlaceParams.address" />
      image_url:
      <input type="img" v-model="newPlaceParams.image_url" />
     <p> <button v-on:click="createPlace()">Create Place</button></p>
      </div>
   <!-- <h1>{{ places }}</h1> -->
   <h3>~All Places~</h3>
   <div v-for="place in places" v-bind:key="place.id">
     <p>{{ place.name }}</p>
     <p>{{ place.address }}</p>
     <img v-bind:src="place.image_url" v-bind:alt="place.name" />
     <button v-on:click="showPlace(place)">More info</button>
  </div>
  <dialog id="place-details">
   <form method="dialog">
     <h1>Place info</h1>
     <p>Name: {{ currentPlace.name }}</p>
     <p>address: {{ currentPlace.address }}</p>
     <p>image_url: {{ currentPlace.image_url }}</p>
     <button>Close</button>
    </form>
  </dialog>
</div>
</template>

<style></style>