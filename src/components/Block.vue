<template>
    <div v-if="showBlock" @click="stopTimer" class="block">Click Me!</div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import {Time} from '../globals'

interface Data {
  showBlock: boolean;
  timer: Time;
  reactionTime: number
}
export default defineComponent({
  name: 'Block',
  props: {
    delay: {
      type: Object as PropType<Time>,
      required: true
    }
  },
  data(): Data {
    return {
      showBlock: false,
      timer: undefined,
      reactionTime: 0
    }
  },
  methods: {
    setShowBlock() {
      this.showBlock = !this.showBlock
      this.startTimer()
    },
    startTimer() {
      this.timer = setInterval(() => this.reactionTime += 10, 10)
    },
    stopTimer() {
      clearInterval(this.timer)
      this.$emit('stopGame', this.reactionTime)
    }
  },
  mounted() {
    setTimeout(() => this.setShowBlock(), this.delay)
  }
})
</script>

<style>
.block {
  width: 25%;
  border-radius: 20%;
  background-color: rgba(182, 37, 37, 0.556);
  color: white;
  padding: 5rem 0;
  margin: 2rem auto;
}

.block:hover {
  cursor: pointer
}
</style>