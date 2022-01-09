<template>
  <div class="chart">
    <div v-for="occurrences in counter" :key="occurrences" class="bar selected"  @click="toggle">
      <span>{{ occurrences }}</span>
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
  data() {
    return {
    }
  },
  methods: {
    setHeight(occurrences) {
      return 100 / 660 * occurrences * 5
    },
    toggle() {
      if (event.target.classList.contains("selected")) {
        event.target.classList.remove("selected");
      } else {
        event.target.classList.add("selected");
      }

    }
  }
}
</script>


<style>
  .chart {
    margin: 0 auto;
    width: 70%;
    height: 220px;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
  }
  .bar {
    width: 10%;
    border-radius: 5px;
    background-color: #d67e8e;
    color: white;
  }
  .bar:hover {
    background-color: #db4863;
  }
  .bar>span {
    display: block;
    transform: translateY(-20px);
    color: black;

  }
  .selected {
    background-color: crimson;
  }
  .b21 {
    height: 72%;
  }
  .b22 {
    height: 59.05%;
  }
  .b23 {
    height: 56.8%;
  }
  .b24 {
    height: 81.05%;
  }
  .b25 {
    height: 23.45%;
  }
  .b26 {
    height: 92.4%;
  }
  .b27 {
    height: 40.9%;
  }
  .b28 {
    height: 74.2%;
  }
  

</style>
