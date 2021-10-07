<template>
  <div class="slider">
    <slot></slot>
    <div class="item-modal__slider-controls">
      <button id="next" @click="slider('next')">→</button>
      <button id="previos" @click="slider('prev')">←</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    slider (action) {
      if (action === 'next') {
        this.$emit('next')
      } else {
        this.$emit('prev')
      }
    }
  }
}
</script>

<style scoped>
.slider {
  position: relative;
  overflow: hidden;
  width: 560px;
  height: 320px;
}
button {
  color: white;
  position: absolute;
  height: 40px;
  width: 50px;
  top: calc(50% - 20px);
  background-color: rgba(0, 0, 0, 0.8);
  border: none;
}

button:focus,
button:hover {
  cursor: pointer;
  outline: none;
}

#next {
  right: 0;
}

#prev {
  left: 0;
}
@media only screen and (max-width: 588px) {
  .slider {
    position: relative;
    overflow: hidden;

    height: 220px;
  }
}
@media only screen and (max-width: 400) {
  .slider {
    height: 120px;
  }
}
</style>
