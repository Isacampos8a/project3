<script setup>
import {ref} from 'vue'

let countdownInterval;
const time = ref(0);
const timerDisplay = ref('Time Left: 0 min 0sec')

//audio
const alarm = new Audio('morning_flower.mp3')

function startTimer() {
    const targetTime = time.value * 60;
    let currentTime = targetTime;



    //clears the countdown
    if (countdownInterval){
        clearInterval(countdownInterval);
    }

    countdownInterval = setInterval(() => {
        const minutesLeft = Math.floor(currentTime / 60);
        const secondsLeft = currentTime % 60;
        timerDisplay.value = `Time Left: ${minutesLeft} min ${secondsLeft} sec`

        if (currentTime == 0) {
            clearInterval(countdownInterval);
            timerDisplay.value = "Time's Up! It has reached peak egg-cellence"
            alarm.play();

        }    
        currentTime--; // decrements the time
    }, 1000); //updates every second

    time.value = ''
    timerDisplay.value = ''
}



 
</script>

<template>
  <main class="app">
    <section class="main-title">
      <h2>Egg Timer</h2>
      <h3>by Isabel Campos</h3>

    </section>

    <section class="time-input">
      <input type="number" placeholder="Enter time in minutes" v-model="time">

      <div class="start-button" >
        <button @click="startTimer">Start</button>
      </div>

    </section>

    <section class="timer-display">
      <div id="timerDisplay">
        <h4>{{timerDisplay}}</h4>
      </div>

    </section>
  </main>
  
</template>


