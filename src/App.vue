<template>
  <div class="whackamole">
    <h1 class="logo">
      Whack-a-mole!
    </h1>
    <button
      class="start-game" @click='startGame'
    >
      Start Game
    </button>
    <div class="counters-container">
      <Counter heading='Score:' :count='score'></Counter>
      <Counter heading='HighScore:' :count='highScore'></Counter>
      <Counter heading='Timer' :count='time'></Counter>
    </div>
    <div class="moles-container gameActive">
      <Mole v-for='(mole, index) in moleData' :isActive='mole.isActive' :key='index'></Mole>
    </div>
  </div>
</template>

<script>
import Counter from './components/Counter';
import Mole from './components/Mole';

export default {
  name: 'App',
  components: {
    Counter: Counter,
    Mole: Mole,
  },
  data: function() {
    return {
      score: 0,
      highScore: 0,
      time: 20,
      moleData: [
        { isActive: true },
        { isActive: false },
        { isActive: true },
        { isActive: true },
      ],
      timerIntervalID: null,
    };
  },
  methods: {
    startGame: function() {
      this.startTimer();
    },
    endGame: function() {
      this.stopTimer();
    },
    startTimer: function() {
      this.time = 20;
      this.timerIntervalID = this.timerIntervalID || setInterval(this.advanceTimer, 1000);
    },
    advanceTimer: function() {
      this.time > 0 ? this.time -= 1 : this.endGame();
    },
    stopTimer: function() {
      clearInterval(this.timerIntervalID);
    },
  }
};
</script>

<style>
.whackamole {
  font-family: 'Bungee', sans-serif;
  max-width: 960px;
  margin: auto;
  text-align: center;
}

.start-game {
  font-family: 'Bungee', sans-serif;
  padding: 20px;
  border-radius: 3px;
  border: 0;
  background-color: #52b1d6;
  color: #fff;
  font-size: 1em;
  cursor: pointer;
}

.counters-container {
  display: flex;
  justify-content: space-evenly;
}

.moles-container {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.moles-container.game-active {
  opacity: 1;
}

.dirt {
  width: 100%;
  margin: auto;
  z-index: 1;
  position: absolute;
  bottom: 0;
}
</style>
