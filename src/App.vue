<script setup>
import { onMounted, ref, provide } from "vue";
import CountryList from "@/components/CountryList.vue";
import SearchCountry from "@/components/SearchCountry.vue";
import FilterList from "./components/FilterList.vue";
import axios from "axios";
const BASE_URL = "https://restcountries.com/v3.1";
const countries = ref([]);
const capitals = ref([]);
const fetchData = async () => {
  axios.get(`${BASE_URL}/all`).then((response) => {
    // console.log("response :>> ", response);
    countries.value = response.data;
    response.data.forEach((item, index) => {
      capitals.value.push({ capital: item.capital, id: index });
    });
  });
};
onMounted(() => {
  fetchData();
});
provide("countries", countries);
provide("capitals", capitals);
</script>
<template lang="pug">
main.container
  div.app
    SearchCountry
    FilterList
    CountryList
    div.flex
      div.item(v-for="(country, index) in countries", :key="country.idd")
        h6 {{ String(capitals[index].capital) }}
        h5 {{ country.name.common }}
        h5 {{ country.population }}
        h5 {{ country.region }}
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
