<script setup>
import { ref, computed } from 'vue'
import GameStatus from '@/components/GameStatus.vue'
import GameBoard from '@/components/GameBoard.vue'
import RestartButton from '@/components/RestartButton.vue'
import dogImg from '@/images/dog.png'
import catImg from '@/images/cat.png'
import bgImg from '@/images/background.jpg'

const WINNING_LINES = [
  [0, 1, 2], [3, 4, 5], [6, 7, 8],
  [0, 3, 6], [1, 4, 7], [2, 5, 8],
  [0, 4, 8], [2, 4, 6],
]

const board = ref(Array(9).fill(null))
const currentPlayer = ref('dog')

const winner = computed(() => {
  for (const [a, b, c] of WINNING_LINES) {
    const cell = board.value[a]
    if (cell && cell === board.value[b] && cell === board.value[c]) {
      return cell
    }
  }
  return null
})

const isDraw = computed(() => {
  if (winner.value) {
    return false
  }
  return board.value.every((cell) => cell !== null)
})

const isGameOver = computed(() => {
  return winner.value !== null || isDraw.value
})

function playerImage(player) {
  if (player === 'dog') {
    return dogImg
  }
  if (player === 'cat') {
    return catImg
  }
  return null
}

const cells = computed(() => {
  return board.value.map((value) => {
    return {
      image: playerImage(value),
      player: value,
      disabled: value !== null || isGameOver.value,
    }
  })
})

const statusText = computed(() => {
  if (winner.value === 'dog') {
    return 'Победили собачки!'
  }
  if (winner.value === 'cat') {
    return 'Победили кошечки!'
  }
  if (isDraw.value) {
    return 'Ничья'
  }
  if (currentPlayer.value === 'dog') {
    return 'Ход собачки'
  }
  return 'Ход кошечки'
})

function makeMove(index) {
  if (isGameOver.value) {
    return
  }
  if (board.value[index] !== null) {
    return
  }
  board.value[index] = currentPlayer.value
  currentPlayer.value = currentPlayer.value === 'dog' ? 'cat' : 'dog'
}

function resetGame() {
  board.value = Array(9).fill(null)
  currentPlayer.value = 'dog'
}
</script>

<template>
  <div class="app" :style="{ backgroundImage: `url(${bgImg})` }">
    <GameStatus :text="statusText" />
    <GameBoard :cells="cells" @move="makeMove" />
    <RestartButton v-if="isGameOver" @restart="resetGame" />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Handjet:wght,ELSH@100..900,2&display=swap');
body {
  font-family: "Handjet", sans-serif;
  margin: 0;
  padding: 0;
}
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 24px;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
</style>
