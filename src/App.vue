<template>
  <h1>Chris Reaction Timer</h1>
  <button class="play-button" @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" :delay="theDelay" @end="endGame" /> <!-- catching emit --> 
  <!-- <Results v-if="gameEnded" time=recordedTime /> -->
  <!-- <p v-if="showRecordedTime">Score: {{formattedTime}} </p> -->
  <Results v-if="showRecordedTime" :time="recordedTime"/> <!--remember to register 'time' prop in Results component-->
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";

export default {
  name: "App",
  components: {
    Block, Results
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      gameEnded: false,
      recordedTime: null,
      showRecordedTime: false
    };
  },
  methods: {
    start() {
      // called when Play button is clicked
      this.theDelay  = Math.random() * 4000 + 1000; // a random number between 1 to 5 seconds`
      this.isPlaying = true;
      this.showRecordedTime = false;
    },
    endGame(theReactionTimeThatWasEmittedByBlock) { // theReactionTimeThatWasEmittedByBlock is automatically passed from @end
      this.recordedTime = theReactionTimeThatWasEmittedByBlock;
      this.isPlaying    = false;
      this.gameEnded    = true;
      this.showRecordedTime = true;
    },
  },
  computed: {
    formattedTime() {
      if (this.recordedTime !== null) {
        return this.recordedTime + 'ms';
      }
      return '';
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
.play-button {
  display: inline-block;
  padding: 12px 24px;
  font-size: 20px;
  font-weight: bold;
  text-transform: uppercase;
  border-radius: 8px;
  background-color: #4CAF50;
  color: #FFFFFF;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.play-button:hover {
  background-color: #45a049;
}

.play-button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}
</style>
