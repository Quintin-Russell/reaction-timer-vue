<template>
<h1>Reaction Timer</h1>
<button @click="startGame" :disabled="isPlaying">Play</button>
<Block v-if="isPlaying" :delay="delay" @stopGame="handleStopGame"/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import {Time} from './globals'
import Block from './components/Block.vue'

interface Data {
  isPlaying: boolean;
  delay: Time;
  score: Time;
}

export default defineComponent({
  name: 'App',
  components: { Block },
  data(): Data {
    return {
      isPlaying: false,
      delay: undefined,
      score: undefined
    }
  },
  methods: {
    startGame() {
      this.delay = 1500 + (5000 * Math.random())
      this.isPlaying = true
    },
    handleStopGame(reactionTime: number) {
      this.score = reactionTime
      this.isPlaying = false
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
</style>
