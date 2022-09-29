<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
/* import * as dotenv from "dotenv";
dotenv.config(); */
//const BASE_URL = process.env.BASE_URL || "https://restcountries.com/v3.1/all";
import { onMounted, ref } from "vue";
import CountryList from "@/components/CountryList.vue";
import SearchCountry from "@/components/SearchCountry.vue";
import FilterList from "./components/FilterList.vue";
const BASE_URL = "https://restcountries.com/v3.1";
const countryList = ref([]);
const fetchData = async () => {
  await fetch(`${BASE_URL}/all`)
    .then((response) => response.json())
    .then((data) => {
      countryList.value = data;
      console.log("data :>> ", data);
      console.log("countryList :>> ", countryList.value);
    });
};
onMounted(() => {
  fetchData();
});
</script>
<template lang="pug">
main.container
  div.app
    h3 Osman
    h3 {{ BASE_URL }}
    SearchCountry
    FilterList
    CountryList
    div.flex
      div.item(v-for="country in countryList" :key="country")
        pre {{ country }}
        h5 {{ country.name.common }}
        h5 {{ country.population }}
        h5 {{ country.region }}
        pre {{ country.capital || "="}}
        img(:src="country.flags.svg", width="30")
</template>

<style scoped>
.flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: row;
  gap: 2rem;
  flex-wrap: wrap;
}
.item {
  border: 1px solid red;
}
</style>

