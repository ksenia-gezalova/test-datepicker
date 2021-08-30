<template>
  <div class="app">
    <datepicker />
  </div>
</template>

<script>
import Datepicker from '@/components/Datepicker';

export default {
  name: 'App',
  components: {
    Datepicker
  }
}
</script>

<style lang="scss" scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}
</style>

<style>
.app {
  font-family: 'Quicksand', sans-serif;
}
</style>