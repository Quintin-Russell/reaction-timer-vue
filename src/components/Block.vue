<template>
  <div @click="handleClick" class="block" v-if="showBlock">Click Me!</div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
type Delay = number|undefined
export default defineComponent({
    name: 'Block',
    props: {
      delay: {
        type: Object as PropType<Delay>,
        required: true
      }
    },
    data() {
      return {
        showBlock: false
      }
    },
    methods: {
      setShowBlock() {
        this.showBlock = !this.showBlock
      },
      handleClick() {
        
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
    background-color:rgba(182, 37, 37, 0.556);
    color: white;
    padding: 5rem 0;
    margin: 2rem auto;
}
</style>