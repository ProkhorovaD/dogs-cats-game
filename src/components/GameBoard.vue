<script setup>
import GameCell from './GameCell.vue'

defineProps(['cells'])
defineEmits(['move'])
</script>

<template>
  <div class="board">
    <GameCell
      v-for="(cell, i) in cells"
      :key="i"
      :cell="cell"
      :index="i"
      @click="(index) => $emit('move', index)"
    />
  </div>
</template>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 8px;
}
</style>
