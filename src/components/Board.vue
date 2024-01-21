<script setup lang="ts">
type Tile = 0 | 1 | null
type Board = Tile[][]

import { onMounted, reactive, ref, defineEmits } from 'vue';

const size = 5
const board = reactive<Board>(Array(size).fill(Array(size).fill(null)))

const emit = defineEmits<{
   (e: 'point'): void
}>()

function updateBoard(row: number, col: number, tile: Tile) {
   board[row] = board[row].map((t, i) => i === col ? tile : t)
}

function startGame() {
   updateBoard(0, 0, 0)
   generatePoint()
}

function findPlayer(): { row: number, column: number } {
   const row = board.findIndex(row => row.includes(0))

   if (row === -1) return { row: -1, column: -1 }

   const column = board[row].findIndex(tile => tile === 0)

   if (column === -1) return { row: -1, column: -1 }

   return { row, column }
}

function generatePoint() {


   let row = Math.floor(Math.random() * size)
   let column = Math.floor(Math.random() * size)

   while (board[row][column] !== null) {
      row = Math.floor(Math.random() * size)
      column = Math.floor(Math.random() * size)
   }

   updateBoard(row, column, 1)
}

function movePlayer(direction: 'up' | 'down' | 'left' | 'right') {
   const player = findPlayer()

   if (player.row === -1 || player.column === -1) return


   let newRow = player.row

   switch (direction) {
      case 'up':
         newRow--
         break
      case 'down':
         newRow++
         break
   }

   if (newRow < 0 || newRow >= size) return


   let newCol = player.column

   switch (direction) {
      case 'left':
         newCol--
         break
      case 'right':
         newCol++
         break
   }

   if (newCol < 0 || newCol >= size) return


   const tile = board[newRow][newCol]

   if (tile === 1) {
      emit('point')
      generatePoint()
   }

   updateBoard(player.row, player.column, null)
   updateBoard(newRow, newCol, 0)
}

onMounted(() => {
   window.addEventListener('keydown', (event) => {
      switch (event.key) {
         case 'w':
         case 'ArrowUp':
            movePlayer('up')
            break
         case 's':
         case 'ArrowDown':
            movePlayer('down')
            break
         case 'a':
         case 'ArrowLeft':
            movePlayer('left')
            break
         case 'd':
         case 'ArrowRight':
            movePlayer('right')
            break
      }

   })
})


startGame()

</script>

<template>
   <main>
      <div class="board">
         <div class="row" v-for="row in board">
            <div :class="{ tile: true, player: tile === 0, point: tile === 1 }" v-for="tile in row">
            </div>
         </div>
      </div>

   </main>
</template>

<style>
.row {
   display: flex;
}

.tile {
   width: 32px;
   height: 32px;
   border-radius: 4px;

   margin: 4px;

   background-color: rgb(31, 47, 27);
}

.player {
   background-color: rgb(45, 200, 0);
}

.point {
   background-color: rgb(240, 244, 4);
}
</style>