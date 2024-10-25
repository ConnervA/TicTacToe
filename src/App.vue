<template>
<div class="h-screen flex justify-center items-center bg-blue-700">
  <Header class="text-5xl font-bold text-white text-center absolute top-10">
    TicTacToe
    <div>{{isPlayer1 ? 'Player 1' : 'Player 2'}}</div>
  </Header>
  <div class="bg-blue-700 w-96 h-96 text-center aspect-square rounded-md shadow-lg">
    <div v-if="isGameWon" class="absolute top-60 left-0 right-0 text-white text-4xl font-bold py-2 rounded-t-md">
      Spieler {{isPlayer1 ? '2' : '1'}} hat gewonnen!
    </div>
    <div class="grid grid-cols-3 gap-4">
      <div v-for="n in tictactoeGrid" class="border-2 border-white aspect-square rounded-md" @click="clickHandler(n.id)">
        <div v-if="n.value === 1" class="w-2/3 h-2/3 mx-auto my-4 rounded-full border-8 border-red-700"></div>
        <div v-else-if="n.value === 2" class="my-1 text-8xl text-red-700">X</div>
        <div v-else></div>
      </div>
    </div>        
  </div>
  <!-- <footer class="w-full bg-blue-700 text-white py-4">
    <div class="flex justify-evenly">
      <div class="text-center font-semibold">Conner von Ahnen</div>
      <div class="text-center font-semibold">Scopvisio FibuNet GmbH</div>
    </div>
  </footer> -->
</div>
<div>
  <button @click="clickNew">Neustart!</button>
</div>
</template>
<script setup lang="ts">
import confetti from 'canvas-confetti';
import { computed, ref } from 'vue';

const tictactoeGrid = ref(
  [
    {id: 1, value: 0 },
    {id: 2, value: 0 },
    {id: 3, value: 0 },
    {id: 4, value: 0 },
    {id: 5, value: 0 },
    {id: 6, value: 0 },
    {id: 7, value: 0 },
    {id: 8, value: 0 },
    {id: 9, value: 0 },
  ]
)

const isPlayer1 = ref(true)

const isGameWon = computed(() => {
  if(
    tictactoeGrid.value[0].value === 1 && tictactoeGrid.value[1].value === 1 && tictactoeGrid.value[2].value === 1 || 
    tictactoeGrid.value[0].value === 2 && tictactoeGrid.value[1].value === 2 && tictactoeGrid.value[2].value === 2 ||
    tictactoeGrid.value[0].value === 1 && tictactoeGrid.value[4].value === 1 && tictactoeGrid.value[8].value === 1 ||
    tictactoeGrid.value[0].value === 2 && tictactoeGrid.value[4].value === 2 && tictactoeGrid.value[8].value === 2 ||
    tictactoeGrid.value[0].value === 1 && tictactoeGrid.value[3].value === 1 && tictactoeGrid.value[6].value === 1 ||
    tictactoeGrid.value[0].value === 2 && tictactoeGrid.value[3].value === 2 && tictactoeGrid.value[6].value === 2 ||
    tictactoeGrid.value[1].value === 1 && tictactoeGrid.value[4].value === 1 && tictactoeGrid.value[7].value === 1 ||
    tictactoeGrid.value[1].value === 2 && tictactoeGrid.value[4].value === 2 && tictactoeGrid.value[7].value === 2 ||
    tictactoeGrid.value[2].value === 1 && tictactoeGrid.value[5].value === 1 && tictactoeGrid.value[8].value === 1 ||
    tictactoeGrid.value[2].value === 2 && tictactoeGrid.value[5].value === 2 && tictactoeGrid.value[8].value === 2 ||
    tictactoeGrid.value[2].value === 1 && tictactoeGrid.value[4].value === 1 && tictactoeGrid.value[6].value === 1 ||
    tictactoeGrid.value[2].value === 2 && tictactoeGrid.value[4].value === 2 && tictactoeGrid.value[6].value === 2 ||
    tictactoeGrid.value[3].value === 1 && tictactoeGrid.value[4].value === 1 && tictactoeGrid.value[5].value === 1 ||
    tictactoeGrid.value[3].value === 2 && tictactoeGrid.value[4].value === 2 && tictactoeGrid.value[5].value === 2 ||
    tictactoeGrid.value[6].value === 1 && tictactoeGrid.value[7].value === 1 && tictactoeGrid.value[8].value === 1 ||
    tictactoeGrid.value[6].value === 2 && tictactoeGrid.value[7].value === 2 && tictactoeGrid.value[8].value === 2 
    ) {
      confettiHandler()
      return true;

    } 
    else {
      return false;
    }
})


function clickHandler(n: number) {
  const foundObject = tictactoeGrid.value.find(obj => obj.id === n);
  console.log(foundObject)
  
  if (foundObject.value === 0 && isGameWon.value === false){
    if (isPlayer1.value){
    foundObject.value = 1
    }
    else{
      foundObject.value = 2
    }
    isPlayer1.value = !isPlayer1.value 
  } 
}

function confettiHandler(){
  confetti({
    particleCount: 500,
    spread: 180,
    origin: { y: 0.6 },
    startVelocity: 60
  });
}

function clickNew(){
  tictactoeGrid.value = [
    {id: 1, value: 0 },
    {id: 2, value: 0 },
    {id: 3, value: 0 },
    {id: 4, value: 0 },
    {id: 5, value: 0 },
    {id: 6, value: 0 },
    {id: 7, value: 0 },
    {id: 8, value: 0 },
    {id: 9, value: 0 },
  ]  
}
</script>