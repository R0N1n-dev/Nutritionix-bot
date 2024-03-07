<template>
  <div>
    <form id="my-form">
      <input type="text" v-model="query" placeholder="Food consumed" />
      <input type="text" v-model="timezone" />
    </form>
    <button @click.prevent="getData">Get</button>

    <div v-if="myResponse !== null">
      {{ myResponse }}
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
import axios from "axios";
const query = ref("");
const timezone = ref("US/Eastern");
const myResponse = ref(null);
function getData() {
  axios({
    method: "POST",
    url: "https://trackapi.nutritionix.com/v2/natural/nutrients",
    headers: {
      "Content-Type": "application/json",
      "x-app-id": import.meta.env.PUBLIC_ID,
      "x-app-key": import.meta.env.PUBLIC_KEY,
    },
    data: {
      query: query.value,
      timezone: timezone.value,
    },
  }).then((response) => {
    myResponse.value = response?.data;
    console.log(response);
  });
}
</script>
