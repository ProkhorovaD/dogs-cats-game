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
  background: rgba(255, 255, 255, 0.85);
  border-radius: 8px;
  font-size: 24px;
  color: #222;
}
</style>
