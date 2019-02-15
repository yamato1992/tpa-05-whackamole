<template>
  <div class="mole-container" :class='moleStatus'>
    <div class="mole-image-container">
      <img class="mole" src="../assets/mole.png" alt="mole" @click='moleClicked' />
    </div>
    <img class="dirt" src="../assets/dirt.svg" alt="mole dirt"/>
  </div>
</template>

<script>
export default {
  name: 'Mole',
  props: {
    isActive: Boolean,
  },
  computed: {
    moleStatus: function() {
      return this.isActive ? 'active' : 'inactive';
    }
  },
  methods: {
    moleClicked: function() {
      this.$emit('mole-clicked', this.index);
    }
  }
};
</script>

<style>
.mole-container {
  width: 160px;
  height: 160px;
  display: inline-block;
  margin: 10px;
  position: relative;
}

.mole-image-container {
  overflow: hidden;
  width: 160px;
  height: 140px;
}

.mole-container img {
  display: block;
  transition: all 0.3s ease;
}

.mole {
  position: relative;
  width: 60%;
  margin: auto;
  cursor: pointer;
}

.mole-container.active .mole {
  /* display: block; */
  top: 0px;
}

.mole-container.inactive .mole {
  top: 200px;
}
</style>
