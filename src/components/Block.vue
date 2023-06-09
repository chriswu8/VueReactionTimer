<template>
  <div class="block" v-if="showBlock" @click="stopTimer">Click Me</div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0
    };
  },
  mounted() {
    // fires when mounted
    console.log("Block component MOUNTED");
    setTimeout(() => {
      this.showBlock = true;
      console.log(this.delay);
    }, this.delay);
  },
  updated() {
    this.startTimer();
    console.log("Block component UPDATED");
  },
  unmounted() {
    console.log("Block component UNMOUNTED");
  },
  methods: {
    startTimer() {
        this.timer = setInterval(() => {
            this.reactionTime += 10;  // increment reactionTime by 10 every 10ms
        }, 10)
    },
    stopTimer() {
        clearInterval(this.timer);
        console.log("reaction time: " + this.reactionTime + " milliseconds");
        this.$emit('end', this.reactionTime)
    }, 
  }
};
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #ffbe90;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>