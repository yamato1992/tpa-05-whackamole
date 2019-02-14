<template>
  <div class="moles-container gameActive">
    <Mole v-for='(mole, index) in moleData' :isActive='mole.isActive' :key='index'></Mole>
  </div>
</template>

<script>
import Mole from './Mole';

export default {
  name: 'Moles',
  components: {
    Mole: Mole,
  },
  data: function() {
    return {
      moleData: [
        { isActive: true },
        { isActive: false },
        { isActive: true },
        { isActive: true },
      ],
    };
  }
};
</script>
