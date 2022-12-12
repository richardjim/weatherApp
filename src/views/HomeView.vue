<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input v-model="searchQuery" type="text" placeholder="Search for a city or state" @input="getSearchResults"
        class="py-2 px-1 w-full bg-transparent border-b focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]" />
      <ul v-if="mapboxSearchResults"
        class="absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1 top-[66px]">
        <li v-for="searchResult in mapboxSearchResults" :key="searchResult.id" class="py-2 cursor-pointer">
          {{ searchResult.place_name }}</li>
      </ul>
    </div>
  </main>
</template> 

<script setup>
import { ref } from 'vue';


const mapboxAPIKey =
  "pk.eyJ1Ijoiam9obmtvbWFybmlja2kiLCJhIjoiY2t5NjFzODZvMHJkaDJ1bWx6OGVieGxreSJ9.IpojdT3U3NENknF6_WhR2Q";

const searchQuery = ref(null);
const queryTimeOut = ref(null);

const mapboxSearchResults = ref(null);
const searchError = ref(null)

const getSearchResults = () => {
  clearTimeout(queryTimeOut.value);
  queryTimeOut.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      const result = await axios.get(
        `https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapboxAPIKey}&types=place`
      );
      mapboxSearchResults.value = result.data.features;
      return;
    }
    mapboxSearchResults.value = null;
  }, 300);
};
</script>
