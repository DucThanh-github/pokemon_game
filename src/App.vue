<template>
  <main-screen v-if="statusMatch==='default'" @onStart="onHandleBeforeStart($event)" />
  <interact-screen v-if="statusMatch==='match'" :cardContext="settings.cardsContext" @onFinish="onGetResult($event)"/>
  <result-screen v-if="statusMatch==='result'" :timer="timer" @onStartAgain="statusMatch = 'default'"/>
  
  <coppy-right-screen/>

</template>
<script>
import MainScreen from './components/MainScreen.vue';
import InteractScreen from './components/InteractScreen.vue';
import ResultScreen from './components/ResultScreen.vue';
import { shuffled } from './utils/array'
import CoppyRightScreen from './components/CoppyRightScreen.vue';
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext:[],
        startedAt: null
      },
      statusMatch: 'default',
      timer: 0
    }
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from({length: this.settings.totalOfBlocks/2}, (_, i)=>i+1)
      const secondCards = [...firstCards]
      const cards = [...secondCards, ... firstCards]
      this.settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))))
      console.log(this.settings.cardsContext, this.settings)
      this.settings.startedAt = new Date().getTime();
      console.log('befor game', config)

      //data really
      this. statusMatch= 'match'
    },
    onGetResult(time) {
      this.timer = time - this.settings.startedAt
      this.statusMatch= 'result'
      console.log('timer',this.timer)
    }
  },
  components: {MainScreen,InteractScreen,ResultScreen, CoppyRightScreen},
};
</script>