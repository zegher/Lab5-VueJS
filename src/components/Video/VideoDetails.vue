<script setup>
    //define properties
    const props = defineProps(["description"]);
</script>

<template>
  <div>
    <h3>Username</h3>
    <p>{{ description }}</p>
  </div>
</template>

<style scoped>
  h1 {
    color: red;
  }
</style>
