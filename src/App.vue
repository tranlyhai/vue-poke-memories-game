<template>
  <main-screen v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart($event)" />
  <interact-screen 
    v-else-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext" 
    @onFinshed="onGetResult()"
    />
  <result-screen 
    v-else-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
    />
  
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from './components/InteractScreen.vue';
import ResultScreen from "./components/ResultScreen.vue";


import { shuffled } from "./utils/array.js";

export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    
  },
  data() {
    return {
      statusMatch: 'default',
      timer: 0,
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startAt: null,
      },
    }
  },
  methods: {
    onHandleBeforeStart: function(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        {length: this.settings.totalOfBlocks/2}, 
        (_i, i) => i + 1
      );
      const secondCards = [...firstCards];
      const card = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(shuffled(shuffled(shuffled(card))));
      this.settings.startAt = new Date().getTime();
      // 
      this.statusMatch = 'match';
    },
    onGetResult: function () {
      // get timmer
      this.timer = new Date().getTime() - this.settings.startAt;
      // switch 
      this.statusMatch = 'result';
    }
  }
}
</script>

<style lang="css" scoped>

</style>
