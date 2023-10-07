<script setup lang="ts">
import DropDown from './components/DropDown.vue';
import SubmitBtn from './components/SubmitBtn.vue';
</script>

<template>
  <div id="app">
    <div id="input-panel">
    <DropDown />
    <SubmitBtn />
  </div>
  </div>
  
</template>

<style scoped>
#app {
  max-width: 1000px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

#input-panel{
  display: flex;
  grid-column-gap: 2em;
}
</style>
