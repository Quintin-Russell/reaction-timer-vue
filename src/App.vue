<template>
  <h1>Reaction Timer</h1>
  <button class='play' v-if="!isPlaying" @click="startGame">Play</button>
  <Block v-if="isPlaying && !showResults" :delay="delay" @stopGame="handleStopGame" />
  <Results v-if="showResults" :score="score" @reset="reset" />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { Time } from './globals'
import Block from './components/Block.vue'
import Results from './components/Results.vue'

interface Data {
  isPlaying: boolean;
  delay: Time;
  score: Time;
  showResults: boolean;
}

export default defineComponent({
  name: 'App',
  components: { Block, Results },
  data(): Data {
    return {
      isPlaying: false,
      delay: undefined,
      score: undefined,
      showResults: false
    }
  },
  methods: {
    setIsPlaying() {
      this.isPlaying = !this.isPlaying
    },
    startGame() {
      this.delay = 1500 + (5000 * Math.random())
      this.setIsPlaying()
      this.showResults = false
    },
    handleStopGame(reactionTime: number) {
      this.score = reactionTime
      this.showResults = true
    },
    reset() {
      this.setIsPlaying()
      this.showResults = false
    }
  }
});
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

.play {
  background-color: rgba(0, 128, 0, 0.506);
  padding: 0.5rem 1rem;
  border-radius: 2rem;
}
</style>
