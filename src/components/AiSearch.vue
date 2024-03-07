<template>
  <div>
    <input type="text" v-model="query" placeholder="Food you wnat info on" />
    <button @click.prevent="getFoodData">Get</button>
    <div v-if="myData !== null">
      {{ myData }}
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
import axios from "axios";
const query = ref("");
const myData = ref(null);
function getFoodData() {
  axios(
    `https://trackapi.nutritionix.com/v2/search/instant?query=${query.value}`,
    {
      headers: {
        "x-app-id": import.meta.env.PUBLIC_ID,
        "x-app-key": import.meta.env.PUBLIC_KEY,
      },
    }
  ).then((response) => {
    //console.log(response.data);
    myData.value = response?.data;
  });
}
</script>
