<template>
  <div>
    <form id="my-form">
      <input type="text" v-model="query" placeholder="Activity and time " />
      <select name="Gender" id="" v-model="gender">
        <option value="Female">Female</option>
        <option value="Male">Male</option>
      </select>
      <input type="text" v-model="weight" placeholder="Weight in kg" />
      <input type="text" v-model="height" placeholder="Height in cm" />
      <input type="text" v-model="age" placeholder="Age" />
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
const gender = ref("");
const weight = ref();
const height = ref();
const age = ref();
const myResponse = ref(null);
function getData() {
  axios({
    method: "POST",
    url: "https://trackapi.nutritionix.com/v2/natural/exercise",
    headers: {
      "Content-Type": "application/json",
      "x-app-id": import.meta.env.PUBLIC_ID,
      "x-app-key": import.meta.env.PUBLIC_KEY,
    },
    data: {
      query: query.value,
      gender: gender.value,
      weight_kg: Number(weight.value),
      height_cm: Number(height.value),
      age: Number(age.value),
    },
  }).then((response) => {
    myResponse.value = response?.data;
    //console.log(response);
  });
}
</script>
