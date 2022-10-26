<template>
  <div class="block">Click Me!</div>
</template>

<script lang="ts">
export default {
    props: ['delay']
}
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