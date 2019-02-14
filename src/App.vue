<template>
  <div class="whackamole">
    <h1 class="logo">
      Whack-a-mole!
    </h1>
    <button
      class="start-game" :disabled='isPlaying' @click='startGame'
    >
      Start Game
    </button>
    <div class="counters-container">
      <Counter heading='Score:' :count='score'></Counter>
      <Counter heading='HighScore:' :count='highScore'></Counter>
      <Counter heading='Timer' :count='time'></Counter>
    </div>
    <Moles @mole-clicked='moleEvent' :moles='moles'></Moles>
  </div>
</template>

<script>
import Counter from './components/Counter';
import Moles from './components/Moles';

const TIME_LIMIT = 20;
const MIN_ACTIVITY_TIME = 1;
const MAX_ACTIVITY_TIME = 2;

export default {
  name: 'App',
  components: {
    Counter: Counter,
    Moles: Moles,
  },
  data: function() {
    return {
      score: 0,
      highScore: 0,
      time: TIME_LIMIT,
      timerIntervalID: null,
      moles: [
        { isActive: false, activityTime: 0 },
        { isActive: false, activityTime: 0 },
        { isActive: false, activityTime: 0 },
        { isActive: false, activityTime: 0 },
      ],
      activateMolesIntervalID: null,
      inactivateMolesIntervalID: null,
      isPlaying: false,
    };
  },
  methods: {
    startGame: function() {
      this.startTimer();
      this.startMoles();
      this.isPlaying = true;
    },
    endGame: function() {
      this.stopTimer();
      this.updateHighScore();
      this.resetScore();
      this.stopMoles();
      this.isPlaying = false;
    },
    startTimer: function() {
      this.time = TIME_LIMIT;
      this.timerIntervalID = setInterval(this.advanceTimer, 1000);
    },
    advanceTimer: function() {
      this.time > 0 ? this.time -= 1 : this.endGame();
    },
    stopTimer: function() {
      clearInterval(this.timerIntervalID);
    },
    updateHighScore: function() {
      this.highScore = this.score > this.highScore ? this.score : this.highScore;
    },
    resetScore: function() {
      this.score = 0;
    },
    startMoles: function() {
      this.activateMolesIntervalID = setInterval(this.activateRandomMole, 1000);
      this.inactivateMolesIntervalID = setInterval(this.inactivateMole, 1000);
    },
    activateRandomMole: function() {
      const index = Math.floor(Math.random() * this.moles.length);
      if (this.moles[index].isActive) {
        this.activateRandomMole();
      } else {
        this.moles[index].isActive = true;
        this.moles[index].activityTime = Math.floor(Math.random() * (MAX_ACTIVITY_TIME - MIN_ACTIVITY_TIME) + MIN_ACTIVITY_TIME);
      }
    },
    inactivateMole: function() {
      this.moles.forEach((mole) => {
        mole.activityTime > 0 ? mole.activityTime -= 1 : mole.isActive = false;
      });
    },
    stopMoles: function() {
      this.moles.forEach((mole) => mole.isActive = false);
      clearInterval(this.activateMolesIntervalID);
      clearInterval(this.inactivateMolesIntervalID);
    },
    moleEvent: function(index) {
      this.score += 1;
      this.moles[index].isActive = false;
      this.moles[index].activityTime = 0;
    }
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
