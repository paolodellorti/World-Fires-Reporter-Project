<template>
  <div>
    <h1>World's Fires Tracker</h1>
    <Days :counter="counter"> </Days>
  </div>
</template>

<script>
  import Days from './components/Days.vue'
  import axios from 'axios'

  export default {
    components: {
      Days
    },
    data() {
      return {
        datas: [],
        filterDatas: [],
        selectedDays: [],
        counter: {}
      }
    },
    mounted() {
      axios
        .get('https://jsonkeeper.com/b/8W8M')
        .then(res => {
          this.datas = res.data;
          this.datas.map(fire => {
            if (!this.selectedDays.includes(fire.date)) {
              this.counter[fire.date] =  1;
              return this.selectedDays.push(fire.date)
            } else {
              this.counter[fire.date] +=  1;
            }
          })
          console.log(this.counter["2020-08-21"]);
        })
    }
  };
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Oswald:wght@500&display=swap');
  
  body {
    text-align: center;
    font-family: 'Oswald', sans-serif;
  }
</style>