<template>
  <div class="wrapper clearfix">
    <players-component
        :scorePlayer="scorePlayer"
        :activePlayer="activePlayer"
        :currentStore="currentStore"
    />
    <ControlComponent
    @handleNewGame="handleNewGame"
    @handleDice="handleDice"
    @handleHoleDice="handleHoleDice"
    />
    <dice-componsnets :dice="dice"/>
    <PopupComponent :isOpenPopup="isOpenPopup" @confirm="confirm"/>
  </div>
</template>

<script setup>
import PlayersComponent from "./components/PlayersComponent.vue";
import ControlComponent from "./components/ControlComponents.vue";
import DiceComponsnets from "./components/DiceComponsnets.vue";
import PopupComponent from "./components/PopupComponent"
import { ref} from "vue";

const isPlaying = ref(false)
let isOpenPopup = ref(false)
let scorePlayer = ref([13,30])
const activePlayer = ref(0)
const currentStore = ref(30)
let dice = ref([1,5])

const confirm = () => {
  isPlaying.value = true
  isOpenPopup.value = false
   scorePlayer.value= [0,0]
  activePlayer.value = 0
  currentStore.value = 0
  dice.value = [6,6]
}

const handleHoleDice = () => {
 if(isPlaying.value){
   console.log('1111')
   const oldScore = scorePlayer.value[activePlayer.value]
   const cloneDataScore = [...scorePlayer.value]
   cloneDataScore.value[activePlayer] = oldScore + currentStore.value
   console.log('cloneDataScore',cloneDataScore)
   console.log('cloneDataScore[activePlayer]', cloneDataScore[activePlayer])
   scorePlayer.value = cloneDataScore.value
 }else {
   alert('Vui lòng nhấn bắt đầu')
 }
}

const changeUser = () => {
  setTimeout(()=>{
    currentStore.value = 0
    activePlayer.value = activePlayer.value === 0 ? 1 : 0
  })
}

const handleDice = () => {
  if (isPlaying.value){
    let dice1 = Math.floor(Math.random()*6) +  1
    let dice2 = Math.floor(Math.random()*6) + 1
    dice.value = [dice1,dice2]
    const startCount = currentStore.value +  dice1 + dice2
    currentStore.value = startCount

    if(dice1 === 1 || dice2 === 1){
      setTimeout(()=>{
        alert(`người chơi số ${activePlayer.value + 1} đã quay vào số 1 `)
        changeUser()
      },10)

    }

  }else {
    alert('Vui lòng nhấn bắt đầu')
  }
}

const handleNewGame = () => {
  isOpenPopup.value = true
}
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

html {
  min-height: 100vh;
  min-width: 100vw;
}

body {
  background-image: url("~@/assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}


</style>
