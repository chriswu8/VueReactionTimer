<template>
  <h2>Your reaction time: {{time}} milliseconds</h2>
  <h3>Your rank: {{rank}}</h3>
</template>

<script>
export default {
  props: ['time'],
  data() {
      return {
        rank: null
      }
  },
  mounted() {
    console.log("RESULTS component is MOUNTED")

    if (this.time < 222) 
    {
      this.rank = "God Speed"
    }
    else if(this.time < 1111) 
    {
      this.rank = "Average Joe"
    }
    else 
    {
      this.rank = "Slowpoke"
    }
  }
}
</script>

<style>

</style>