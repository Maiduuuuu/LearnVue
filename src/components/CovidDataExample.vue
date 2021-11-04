<template>
    <div>
        <div class="columns">
            <div class="column">
                <input type="text" class="input mb-3" v-model="search">
            </div>
                <div class="column is-2" >
                    <div class="select ">
                        <select v-model="sort">
                            <option v-for="sorting in sortingFields" :key="sorting.name" :value="sorting">{{sorting.name}}</option>
                        </select>
                    </div>
                </div>
        </div>
        <div class="columns is-multiline">
            <div class="column is-one-fifth" v-for="country in sortedCountries" :key="country.ID">
                <covid-card :country="country"></covid-card>
            </div>
        </div>
    </div>
</template>

<script>
import CovidCard from './CovidCard.vue'
const axios = require('axios');
export default {
  components: { CovidCard },
  created(){
      axios.get('https://api.covid19api.com/summary').then(response => {
          console.log(response);
          this.countries = response.data.Countries;
      });
  },
  data(){
      return {
          countries: [],
          search: '',
          sort: {field: 'Total Confirmed', name: 'Total Confirmed Ascending', order: 'asc'},
          fields: ['TotalConfirmed', 'TotalDeaths', 'NewConfirmed', 'NewDeaths']
      }
  },
  computed: {
      filteredCountries(){
          return this.countries.filter(country => {
              let partialName = country.Country.substr(0,this.search.length);
              return partialName.toLowerCase() == this.search.toLowerCase();
          });
      },
      sortingFields(){
          let sorting = [];
          this.fields.forEach(field =>{
              sorting.push({name: field + ' ascending', order: 'asc', field: field});
              sorting.push({name: field + ' descending', order: 'desc', field: field});              
          });
          return sorting;
      },
      sortedCountries(){
          return this.filteredCountries.sort( (a, b) => {
              let order=this.sort.order == 'desc' ? -1 : 1;
              if(a[this.sort.field] > b[this.sort.field]) {
                  return 1 * order;
              } else if (a[this.sort.field] < b[this.sort.field]) {
                  return -1 * order;
              }
              return 0;
          });
      }
  }

}
</script>

<style>
.w-100{
    width: 100%;
}
</style>