<script setup>
defineProps(['cell', 'index'])
defineEmits(['click'])
</script>

<template>
  <button
    class="cell"
    :disabled="cell.disabled"
    @click="$emit('click', index)"
  >
    <img
      v-if="cell.image"
      :src="cell.image"
      class="cell__image"
      :class="`cell__image--${cell.player}`"
    />
  </button>
</template>

<style scoped>
.cell {
  width: 100px;
  height: 100px;
  padding: 0;
  border: 2px solid #333;
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.85);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.15s ease;
}

.cell:hover:not(:disabled) {
  background: rgba(255, 255, 255, 1);
}

.cell:disabled {
  cursor: default;
}

.cell__image {
  object-fit: contain;
}

.cell__image--cat {
  width: 80%;
  height: 80%;
}

.cell__image--dog {
  width: 95%;
  height: 95%;
}
</style>
