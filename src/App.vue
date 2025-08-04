<template>
  <div class="app">
    <EquipmentList/>
  </div>
</template>

<script>
import EquipmentList from './components/EquipmentList.vue'

export default {
  name: 'app',
  components: {
    EquipmentList
  }
}
</script>

<style>
.app {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100vh;
  overflow-x: auto;
}

* {
  box-sizing: border-box;
}
</style>
