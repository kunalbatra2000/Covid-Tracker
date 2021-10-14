<template>
  <main v-if="!loading"><DataTitle :title="title" :date="dataDate"/>
  <DataBoxes :stats="stats"/>
  <CountrySelect @get-country="getCountryData" :countries="countries" />
  <button @click="clearData()" v-if="stats.Country" class="bg-green-700 text-white rounded p-2 mt-10 mb-8 focus:outline-none hover:bg-green-600 flex flex-col align-center justify-center text-center">Clear Country</button>
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" alt="" srcset="" class="w-24 m-auto"/>
  </main>
  
</template>



<script>
import DataTitle from '././DataTitle.vue'
import DataBoxes from './DataBoxes.vue'
import CountrySelect from './CountrySelect.vue'
export default {
  name: "Home",
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("C:/Users/HP/Desktop/CovidTracker-Vue/covid_tracker/public/hourglass.gif"),
    };
  },
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = res.json();
      return data;
    },
    getCountryData(country){
      this.stats=country;
      this.title=country.Country;
    },
    async clearData() {
      this.loading=true;
      const data=await this.fetchCovidData()
      this.stats=data.Global;
      this.title='Global';
      this.loading=false;
    }
  },
  async created() {
    const data=await this.fetchCovidData();
    this.dataDate=data.Date;
    this.stats=data.Global;
    this.countries=data.Countries;
    this.loading=false;
    console.log(data);
    console.log(data.Date);
    console.log(data.Countries);
  },
};
</script>
