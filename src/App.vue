<template>
  <main-screen v-if="statusMatch==='default'" @onStart="onHandleBeforeStart($event)" />
  <interact-screen v-if="statusMatch==='match'" :cardContext="settings.cardsContext"/>
</template>
<script>
import MainScreen from './components/MainScreen.vue';
import InteractScreen from './components/InteractScreen.vue';
import { shuffled } from './utils/array'
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext:[],
        startedAt: null
      },
      statusMatch: 'default'
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

    }
  },
  components: {MainScreen,InteractScreen},
};
</script>