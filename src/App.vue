<template>
  <div class="whackamole">
    <h1 class="logo">
      Whack-a-mole!
    </h1>
    <button
      class="start-game"
    >
      Start Game
    </button>
    <div class="counters-container">
      <Counter></Counter>
      <Counter></Counter>
      <Counter></Counter>
    </div>
    <div class="moles-container gameActive">
      <Mole></Mole>
      <Mole></Mole>
      <Mole></Mole>
      <Mole></Mole>
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
