<template>
  <MainScreen v-if="status === 'default'" @onStart="onHandleBeforeStart($event)" />
  <InteractScreen
    v-if="status === 'match'"
    :cardContext="settings.cardContext"
    @onFinish="onGetResult"
  />
  <ResultScreen v-if="status === 'result'" :timer="timer" @onStartAgain="status = 'default'"/>
  <Copyright />
</template>

<script>
import Copyright from "./components/CopyRight.vue";
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffer } from "./utils/array.js";
import ResultScreen from "./components/ResultScreen.vue"
export default {
  name: "App",
  components: { Copyright, MainScreen, InteractScreen, ResultScreen },
  data() {
    return {
      status: "default",
      settings: {
        totalBlocks: 0,
        cardContext: [],
        startAt: null,
      },
      timee: 0
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log(config);
      this.status = "match";
      this.settings.totalBlocks = config.totalBlocks;

      const firstCard = Array.from(
        { length: this.settings.totalBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCard = [...firstCard];

      const totalCard = [...firstCard, ...secondCard];
      this.settings.cardContext = shuffer(shuffer(shuffer(shuffer(totalCard))));
      console.log(totalCard);

      this.settings.startAt = new Date().getTime();
    },
    onGetResult() {
      //get timer and switch result screen component
      this.timer = new Date().getTime() - this.settings.startAt;
      this.status = "result";
    }
  },
};
</script>