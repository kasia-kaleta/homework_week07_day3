<template>

    <div>
      <h1>Countries</h1>
      <div class="main-container">
        <countries-list :countries='countries'></countries-list>
        <country-detail :country='selectedCountry'></country-detail>

      </div>
    </div>

</template>

<script>
import { eventBus } from './main.js';
import CountriesList from './components/CountriesList.vue';
import CountryDetail from './components/CountryDetail.vue';
import ListComponent from './components/ListComponent.vue'


export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null
    };
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country;
    })
  },
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail,
  }
}

</script>

<style>
  .main-container {
    display: flex;
    justify-content: space-between;
    font-family: Tahoma, Geneva, sans-serif;
    background-color: paleturquoise;
    text-decoration: none;
  }

</style>
