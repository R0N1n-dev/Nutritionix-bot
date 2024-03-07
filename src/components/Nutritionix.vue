<template>
  <div class="about">
    <h1>
      This is the page for asking the nutrition AI anything inthe related
      options
    </h1>
    <div class="tab-buttons">
      <button
        v-for="(tab, index) in tabs"
        :key="index"
        @click="currentTab = tab.component"
      >
        {{ tab.label }}
      </button>
    </div>
    <component :is="currentTab"></component>
  </div>
</template>

<script setup>
import AI from "./AI.vue";
import Exercise from "./Exercise.vue";
import AiSearch from "./AiSearch.vue";
import { shallowRef, ref, markRaw } from "vue";
const currentTab = shallowRef(AI);
const tabs = ref([
  { label: "Nutrient Search", component: markRaw(AI) },
  { label: "Exercise", component: markRaw(Exercise) },
  { label: "Food Search", component: markRaw(AiSearch) },
]);
</script>

<style>
button {
  margin: 0.4rem 0.5rem;
}
</style>
