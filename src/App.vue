<script setup lang="ts">
import { ref } from 'vue'
import Board from './components/Board.vue'
import Keyboard from './components/Keyboard.vue'

const score = ref(0)


</script>

<template>
   <header>
      <h2 id="score">
         {{ score }}
      </h2>
   </header>
   <Board @point="() => score++" />

   <Keyboard />
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Barlow:wght@400;700&display=swap');

* {
   margin: 0;
   padding: 0;
   box-sizing: border-box;

   font-family: 'Barlow', sans-serif;
}

#app {
   background-color: rgb(30, 30, 30);
   height: 100vh;

   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: center;
}

h2#score {
   color: white;
   font-size: 64px;
   margin-bottom: 16px;
}
</style>
