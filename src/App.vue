<template>
  <div>
    <h1>World's Fires Tracker</h1>
    <Days :counter="counter" :selectedDays="selectedDays" :key="key" @changeFilter="changeFilter" />
    <Map :filtered="filtered" />
  </div>
</template>

<script>
  import Days from './components/Days.vue'
  import Map from './components/Map.vue'
  import axios from 'axios'

  export default {
    components: {
      Days,
      Map
    },
    data() {
      return {
        datas: [],
        filtered: [],
        selectedDays: [],
        counter: {},
        key: 0
      }
    },
    methods: {
      changeFilter(filter) {
        if (this.selectedDays.includes(filter)) {
          let index = this.selectedDays.indexOf(filter);
          this.selectedDays.splice(index, 1)
        } else {
          this.selectedDays.push(filter)
        }
        this.filterData()
      },
      filterData() {
        if (this.selectedDays.length === 8) {
          this.filtered = this.datas
        } else {
          this.filtered = this.datas.filter(fire => {
            if (this.selectedDays.includes(fire.date)) {
              return fire
            }
          })
        }
        console.log(this.filtered);
      }
    },
    mounted() {
      axios
        .get('https://jsonkeeper.com/b/8W8M')
        .then(res => {
          this.datas = res.data
          this.filtered = res.data
          this.datas.map(fire => {
            if (!this.selectedDays.includes(fire.date)) {
              this.counter[fire.date] =  1
              return this.selectedDays.push(fire.date)
            } else {
              this.counter[fire.date] +=  1
            }
          })
          this.key++
        })
    }
  };
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Oswald:wght@500&display=swap');
  
  body {
    text-align: center;
    font-family: 'Oswald', sans-serif;
    margin: 0;
    box-sizing: border-box;
  }
</style>