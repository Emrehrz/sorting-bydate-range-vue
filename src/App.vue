<template>
  <div id="app">
    <Datepicker
      md="4"
      style="width: auto"
      v-model="dateRange"
      placeholder="Tarih Aralığı"
      :enable-time-picker="false"
      range
      :format="dateFormat"
    />
    <br />
    <button @click="filterByDate">getir</button>
    <br />
    <table>
      <tr>
        <th>supplier</th>
        <th></th>
        <th>price</th>
        <th></th>
        <th>income</th>
        <th></th>
        <th>date</th>
      </tr>
      <tr v-for="(row, index) in filteredItems" :key="index">
        <td>{{ row.supplier }}</td>
        <td></td>
        <td>{{ row.price }}</td>
        <td></td>
        <td>{{ row.income }}</td>
        <td></td>
        <td>{{ row.date }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import Datepicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';
import moment from 'moment';

export default {
  name: 'App',
  components: {
    Datepicker,
  },
  data() {
    return {
      startDate: '',
      endDate: '',
      someDate: '',
      dateRange: '',
      dates: '',
      dateFormat: 'dd-MM-yyyy',
      filteredItems: this.works,
      works: [
        {
          supplier: 'Fritsch-Ryan',
          price: 97,
          cost: 14,
          category: 'Green',
          income: 6,
          date: '2023-01-08T14:52:54Z',
        },
        {
          supplier: 'Erdman-Hansen',
          price: 35,
          cost: 67,
          category: 'Mauv',
          income: 39,
          date: '2023-01-03T03:07:57Z',
        },
        {
          supplier: 'Turner-Robel',
          price: 16,
          cost: 54,
          category: 'Violet',
          income: 76,
          date: '2023-02-01T06:10:27Z',
        },
      ],
    };
  },
  methods: {
    getDate() {
      this.dates = this.dateRange.toString().split(',');
      this.startDate = new Date(this.dates[0]);
      this.endDate = new Date(this.dates[1]);

      console.log('Başlangıç tarihi', this.startDate);

      console.log('Bitiş tarihi', this.endDate);

      console.log('moment(): ', moment().format('DD-MM-YYYY'));
    },
    filterByDate() {
      this.filteredItems = this.works.filter((row) => {
        return moment(row.date).isBetween(this.startDate, this.endDate);
      });
      this.works = this.filteredItems;
    },
  },
  computed: {},
  watch: {
    dateRange(newValue, oldValue) {
      this.dates = this.dateRange.toString().split(',');
      this.startDate = new Date(this.dates[0]);
      this.endDate = new Date(this.dates[1]);
      console.log('Başlangıç tarihi', this.startDate);
      console.log('Bitiş tarihi', this.endDate);
      filterByDate();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
