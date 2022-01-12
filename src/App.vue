<template>
  <div class="main">
    <h1>World's Fires Tracker</h1>
    <span>Check every 🔥fire in the world between 21 and 28 August 2020.</span>
    <span>Select or deselect the days you prefer by clicking on them.</span>
    <DaysItem :counter="counter" :selectedDays="selectedDays" :key="key" @changeFilter="changeFilter" />
    <ControllerItem :days="selectedDays.length" :fires="filteredDatas.length" @changeFilter="changeFilter" />
    <MapItem :filteredDatas="filteredDatas" />
  </div>
</template>

<script>
  import DaysItem from './components/DaysItem.vue'
  import ControllerItem from './components/ControllerItem.vue'
  import MapItem from './components/MapItem.vue'
  import axios from 'axios'

  export default {
    components: {
      DaysItem,
      ControllerItem,
      MapItem
    },
    data() {
      return {
        datas: [],
        filteredDatas: [],
        selectedDays: [],
        counter: {},
        key: 0
      }
    },
    methods: {
      changeFilter(filter) {
        if (filter === 'deselectAll') {
          this.selectedDays = []
        } else if (filter === 'selectAll') {
          this.selectedDays = Object.keys(this.counter)
        } else {
          if (this.selectedDays.includes(filter)) {
            let index = this.selectedDays.indexOf(filter);
            this.selectedDays.splice(index, 1)
          } else {
            this.selectedDays.push(filter)
          }        
        }
        this.filterData()
      },
      filterData() {
        if (this.selectedDays.length === 8) {
          this.filteredDatas = this.datas
        } else {
          this.filteredDatas = this.datas.filter(fire => {
            if (this.selectedDays.includes(fire.date)) {
              return fire
            }
          })
        }
      }
    },
    computed: {

    },
    mounted() {
      axios
        .get('https://api.npoint.io/445bc75f908957f14039')
        .then(res => {
          this.datas = res.data
          this.filteredDatas = res.data
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
  }
  .main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
  }
</style>