<template>
  <div id="App">
    <div class="timerContainer">
      <!-- рендерим новый блок секундомера и компоненты stopwatch -->
      <stopwatch v-for="stopwatch in timerCounter" :key="stopwatch"/>
      <div class="addStopwatch" v-on:click="addStopwatch()">
        <div class="plus"></div>
      </div>
    </div>
  </div>
</template>

<script>
import stopwatch from '@/components/stopwatch.vue';
export default {
  name: 'App',
  data: () => ({
    // количество секундомеров на странице
    timerCounter: 0,
  }),
  components: {
    stopwatch,
  },
  methods: {
    // добавляем новый секундомер на страницу
    addStopwatch() {
      this.timerCounter += 1;
    },
  },
};
</script>

<style>
  html{
    height: 100%;
    background-color: #353638;
}
  #app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    display: flex;
    justify-content: center;
    margin-top: 100px;
    align-items: center;
    flex-direction: row;
    width: 900px;
  }
  /*условия для смени положения новых контеров сеундомера при изменени разрешения*/
  /*самое маленькое резрешение, при этом условие все секундомеры появляеться друг под другом*/
  @media (min-width: 320px) and (max-width: 767px) {
    #app {
      width: 300px;
    }
  }
  /*только два в один ряд*/
  @media (min-width: 768px) and (max-width: 1023px) {
    #app {
      width: 600px;
    }
  }    
  /*три в один ряд*/
  @media  (min-width:1024px) {
    #app {
      width: 900px;
    }
  }

  .timerContainer{
    height: auto;
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    padding-left: 50px;
  }
  .addStopwatch{
    width: 225px;
    height: 120px;
    background-color: #696969;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-right: 50px;
    margin-bottom: 25px;
  }
  .plus{
    display:inline-block;
    width:40px;
    height:40px;
    background:
    linear-gradient(#9E9E9E,#9E9E9E),
    linear-gradient(#9E9E9E,#9E9E9E);
    background-position:center;
    background-size: 50% 3px,3px 50%;
    background-repeat:no-repeat;
  }

</style>