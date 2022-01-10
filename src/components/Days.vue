<template>
  <div class="chart">
    <div class="grid">
      <div> <span>120</span> </div>
      <div> <span>90</span> </div>
      <div> <span>60</span> </div>
      <div> <span>30</span> </div>
    </div>
    <div v-for="occurrences, day in counter" 
      :key="occurrences" 
      :style="{height: setHeight(occurrences) + '%'}" 
      class="bar" 
      :class="setColor(occurrences)"  
      @click.self="toggle"
      :data-day="day">
        <span class="occurences">{{ occurrences }}</span>
        <span class="day">Aug {{ day.slice(-2) }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Days',
  props: {
    counter: {
      type: Object
    }
  },
  methods: {
    setHeight(occurrences) {
      return 100 / 660 * occurrences * 5
    },
    setColor(occurrences) {
      if (occurrences < 55) {
        return "level1"
      } else if (occurrences > 55 && occurrences < 80) {
        return "level2"
      } else if (occurrences > 80 && occurrences < 100) {
        return "level3"
      } else {
        return "level4"
      }
    },
    toggle() {
      if (event.target.classList.contains("deselected")) {
        event.target.classList.remove("deselected");
      } else {
        event.target.classList.add("deselected");
      }
      this.$emit('changeFilter', event.target.getAttribute('data-day'))
    }
  }
}
</script>


<style>
  .chart {
    margin: 0 auto;
    margin-bottom: 50px;
    width: 70%;
    height: 220px;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    position: relative;
  }
  .grid {
    position: absolute;
    transform: translateX(-8%);
    top: 0;
    height: 100%;
    width: 108.5%;
    z-index: -10;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    flex-direction: column;
  }
  .grid>div {
    width: 100%;
    height: 22%;
    border-top: 1px solid #afafaf;
    position: relative;
  }
  .grid>div>span {
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    color: #d6d6d6;
  }
  .bar {
    width: 10%;
    border-radius: 5px;
    position: relative;
  }
  .occurences {
    display: block;
    transform: translateY(-20px);
  }
  .day {
    width: 100%;
    display: block;
    position: absolute;
    bottom: -18px;
    font-size: 0.8rem;
    color: #d6d6d6;
  }
  .level1 {
    background-color: rgba(255, 180, 67, 0.85);
    transition: all 0.2s;
  }
  .level1:hover {
    background-color: rgba(255, 165, 31, 0.5);
    transition: all 0.2s;
  }
  .level2 {
    background-color: rgba(255, 114, 20, 0.85);
    transition: all 0.2s;
  }
  .level2:hover {
    background-color: rgba(255, 118, 20, 0.5);
    transition: all 0.2s;
  }
  .level3 {
    background-color: rgba(244, 70, 17, 0.85);
    transition: all 0.2s;
  }
  .level3:hover {
    background-color: rgba(244, 69, 16, 0.5);
    transition: all 0.2s;
  }
  .level4 {
    background-color: rgba(255, 35, 1, 0.85);
    transition: all 0.2s;
  }
  .level4:hover {
    background-color: rgba(255, 35, 1, 0.5);
    transition: all 0.2s;
  }
  .deselected {
    color: #d6d6d6;
    background-color: rgba(170, 170, 170, 0.85);
    font-size: 0.8rem; 
    width: 9%;
    transition: all 0.2s;
  }
  .deselected:hover {
    background-color: rgba(170, 170, 170, 0.5);
    transition: all 0.2s;
  }

</style>
