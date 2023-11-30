<template>
  <div class="container">
    <adicionar />
  </div>
</template>
<script>
import adicionar from './components/adicionar.vue'
export default {
  components: { adicionar },
  
}
</script>
<style>
    .container{
      display: flex;
      justify-content: space-between;
      height: 100vh;
      overflow-x: hidden;
    }
</style>