<script setup lang="ts">
import { ref } from 'vue'

const victory = ref(false)
const turn = ref(true)
const gameBoard = ref(Array<null | boolean>(null, null, null, null, null, null, null, null, null))

const checkState = (pos: number): boolean => {
  const gb = gameBoard.value
  const rowStart = Math.floor(pos / 3) * 3

  // Check if row victory.
  if (
    gb[rowStart] !== null &&
    gb[rowStart] === gb[rowStart + 1] &&
    gb[rowStart] === gb[rowStart + 2]
  ) {
    return true
  }
  // Check if column victory.
  if (gb[pos] === gb[(pos + 3) % 9] && gb[pos] === gb[(pos + 6) % 9]) {
    return true
  }
  // Check diagonal victory.
  if (gb[4] !== null && gb[4] === gb[2] && gb[4] === gb[6]) {
    return true
  }
  if (gb[4] !== null && gb[4] === gb[0] && gb[4] === gb[8]) {
    return true
  }

  return false
}

const takeTurn = (index: number) => {
  if (index >= gameBoard.value.length || gameBoard.value[index] !== null) {
    return
  }

  gameBoard.value[index] = turn.value
  turn.value = !turn.value
  victory.value = checkState(index)
}

const reset = () => {
  for (let i = 0; i < 9; i++) {
    gameBoard.value[i] = null
  }
  turn.value = true
  victory.value = false
}
</script>

<template>
  <div class="game_screen">
    <!-- Board shown. -->
    <div v-if="!victory" class="game_board">
      <div class="game_row">
        <button :disabled="gameBoard[0] !== null" @click="takeTurn(0)" class="no_left no_top">
          {{ gameBoard[0] === null ? ' ' : gameBoard[0] ? 'X' : 'O' }}
        </button>
        <button :disabled="gameBoard[1] !== null" @click="takeTurn(1)" class="no_top">
          {{ gameBoard[1] === null ? ' ' : gameBoard[1] ? 'X' : 'O' }}
        </button>
        <button :disabled="gameBoard[2] !== null" @click="takeTurn(2)" class="no_top no_right">
          {{ gameBoard[2] === null ? ' ' : gameBoard[2] ? 'X' : 'O' }}
        </button>
      </div>
      <div class="game_row">
        <button :disabled="gameBoard[3] !== null" @click="takeTurn(3)" class="no_left">
          {{ gameBoard[3] === null ? ' ' : gameBoard[3] ? 'X' : 'O' }}
        </button>
        <button :disabled="gameBoard[4] !== null" @click="takeTurn(4)">
          {{ gameBoard[4] === null ? ' ' : gameBoard[4] ? 'X' : 'O' }}
        </button>
        <button :disabled="gameBoard[5] !== null" @click="takeTurn(5)" class="no_right">
          {{ gameBoard[5] === null ? ' ' : gameBoard[5] ? 'X' : 'O' }}
        </button>
      </div>
      <div class="game_row">
        <button :disabled="gameBoard[6] !== null" @click="takeTurn(6)" class="no_left no_bottom">
          {{ gameBoard[6] === null ? ' ' : gameBoard[6] ? 'X' : 'O' }}
        </button>
        <button :disabled="gameBoard[7] !== null" @click="takeTurn(7)" class="no_bottom">
          {{ gameBoard[7] === null ? ' ' : gameBoard[7] ? 'X' : 'O' }}
        </button>
        <button :disabled="gameBoard[8] !== null" @click="takeTurn(8)" class="no_right no_bottom">
          {{ gameBoard[8] === null ? ' ' : gameBoard[8] ? 'X' : 'O' }}
        </button>
      </div>
    </div>

    <!-- Game Over. -->
    <div v-else class="winner_winner">
      <p>{{ !turn ? 'CROSS VICTORY' : 'NAUGHT VICTORY' }}</p>
    </div>
    <button @click="reset" class="reset_button">reset</button>
  </div>
</template>

<style scoped></style>
