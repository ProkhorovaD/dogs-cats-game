<script setup>
defineEmits(['restart'])
</script>

<template>
  <button class="restart" @click="$emit('restart')">Начать заново</button>
</template>

<style scoped>
.restart {
  padding: 12px 28px;
  font-size: 32px;
  border: 0px;
  color: white;
  border-radius: 8px;
  background: #ed1afc;
  cursor: pointer;
  transition: background 0.15s ease;
}

.restart:hover {
  background: #cf33ff;
}
</style>
