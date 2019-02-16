<template>
  <div class="moles-container" :class = "{'game-active': isPlaying}">
    <Mole v-for='(mole, index) in moles' :isActive='mole.isActive' :key='index' @mole-clicked='moleClicked(index)'></Mole>
  </div>
</template>

<script>
import Mole from './Mole';

export default {
  name: 'Moles',
  components: {
    Mole,
  },
  props: {
    moles: Array,
    isPlaying: Boolean,
  },
  methods: {
    moleClicked: function(index) {
      this.$emit('mole-clicked', index);
    }
  }
};
</script>

<style>
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
</style>

