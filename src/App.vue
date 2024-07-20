<template>
  <h1>Hello World</h1>
  <p>High Score:{{ highScore }}</p>
  <button @click="start" :disabled="isPlaying">play</button>
  <p v-if="showResult">Reaction time: {{ score }} ms</p>
  <Block v-if="isPlaying" :delay="delay" @end="endGame"/>
  <p v-if="result=='fast'">You are Fast!</p>
  <p v-if="result=='normal'">Not bad!</p>
  <p v-if="result=='slow'">Too Slow!</p>
</template>

<script>
import Block from './components/Block.vue'
export default {
  name: 'App',
  components: {Block},
  data() {
    return {
      delay: null,
      highScore: 0,
      isPlaying: false,
      showResult: false,
      result: null,
      score: null
    }
  },
  methods: {
    start() {
      this.showResult = false
      this.result = null
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
    },
    endGame(reactionTime) {
      this.isPlaying = false
      this.score = reactionTime
      this.showResult = true

      if (this.highScore == 0) {
        this.highScore = this.score
      }
      else if (this.score < this.highScore){
        this.highScore = this.score
      }

      if (this.score < 300) {
        this.result = 'fast'
      }
      else if (this.score < 1000) {
        this.result = 'normal'
      }
      else {
        this.result = 'slow'
      }
    }
  }
}
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
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button:disabled {
  background: black;
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
