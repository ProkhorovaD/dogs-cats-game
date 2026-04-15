<script setup>
defineProps(['text'])
</script>

<template>
  <h2 class="status">{{ text }}</h2>
</template>

<style scoped>
.status {
  margin: 0;
  padding: 12px 24px;
  background: #ed1afc;
  border-radius: 8px;
  font-size: 24px;
  color: white;
}
</style>
