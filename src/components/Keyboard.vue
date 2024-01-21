<script setup lang="ts">
import { reactive, onMounted } from 'vue'
import ArrowUp from './icons/ArrowUp.vue'
import ArrowLeft from './icons/ArrowLeft.vue'
import ArrowDown from './icons/ArrowDown.vue'
import ArrowRight from './icons/ArrowRight.vue'


const pressing = reactive({
   up: false,
   down: false,
   left: false,
   right: false
})

onMounted(() => {
   window.addEventListener('keydown', (event) => {
      switch (event.key) {
         case 'w':
         case 'ArrowUp':
            pressing.up = true
            break
         case 's':
         case 'ArrowDown':
            pressing.down = true
            break
         case 'a':
         case 'ArrowLeft':
            pressing.left = true
            break
         case 'd':
         case 'ArrowRight':
            pressing.right = true
            break
      }

   })

   window.addEventListener('keyup', (event) => {
      switch (event.key) {
         case 'w':
         case 'ArrowUp':
            pressing.up = false
            break
         case 's':
         case 'ArrowDown':
            pressing.down = false
            break
         case 'a':
         case 'ArrowLeft':
            pressing.left = false
            break
         case 'd':
         case 'ArrowRight':
            pressing.right = false
            break
      }
   })
})

</script>

<template>
   <div id="Keyboard">
      <div :class="{ key: true, active: pressing.up }">
         <ArrowUp />
      </div>
      <br />
      <div :class="{ key: true, active: pressing.left }">
         <ArrowLeft />
      </div>
      <div :class="{ key: true, active: pressing.down }">
         <ArrowDown />
      </div>
      <div :class="{ key: true, active: pressing.right }">
         <ArrowRight />
      </div>
   </div>
</template>

<style scoped>
#Keyboard {
   margin-top: 32px;
   text-align: center;
}

.key {
   width: 40px;
   height: 40px;
   background-color: rgba(255, 255, 255, 0.08);
   border-radius: 8px;
   display: inline-flex;
   align-items: center;
   justify-content: center;
   margin: 4px;
   border: 4px solid rgba(255, 255, 255, 0.04);

   color: rgb(30, 30, 30);
   font-size: 20px;

}

.key.active {
   background-color: rgba(255, 255, 255, 0.3);
   border: 4px solid rgba(255, 255, 255, 0.15);
}
</style>