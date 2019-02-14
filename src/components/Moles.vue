<template>
  <div class="moles-container gameActive">
    <Mole v-for='(mole, index) in moles' :isActive='mole.isActive' :index='index' :key='index' @mole-clicked='moleClicked'></Mole>
  </div>
</template>

<script>
import Mole from './Mole';

export default {
  name: 'Moles',
  components: {
    Mole: Mole,
  },
  props: {
    moles: Array,
  },
  methods: {
    moleClicked: function(index) {
      this.$emit('mole-clicked', index);
    }
  }
};
</script>
