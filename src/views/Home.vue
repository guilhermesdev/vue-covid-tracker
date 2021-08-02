<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelect
      @get-country="getCountryData"
      :countries="countries"
    />

    <button
      @click="clearCountryData"
      v-if="stats.Country"
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
    >
      Show global data
    </button>
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching data...
    </div>
    <i class="fas fa-spinner fa-spin text-5xl m-auto"></i>
  </main>
</template>

<script>
import DataTitle from '@/components/DataTitle';
import DataBoxes from '@/components/DataBoxes';
import CountrySelect from '@/components/CountrySelect';

import { ref } from 'vue';

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  setup(){
    const loading = ref(true);
    const title = ref('Global');
    const dataDate = ref('');
    const stats = ref({});
    const countries = ref([]);

    const fetchCovidData = async () => {
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    }

    const getCountryData = country => {
      stats.value = country;
      title.value = country.Country;
    }

    const clearCountryData = async () => {
      loading.value = true;
      const data = await fetchCovidData();

      title.value = 'Global';
      stats.value = data.Global;

      loading.value = false;
    }

    const start = async () => {
      const data = await fetchCovidData();

      dataDate.value = data.Date;
      stats.value = data.Global;
      countries.value = data.Countries;
      loading.value = false;
    };

    start();

    return {
      loading,
      title,
      dataDate,
      stats,
      countries,
      getCountryData,
      clearCountryData
    };
  }
}
</script>
