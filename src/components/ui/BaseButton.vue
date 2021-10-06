<template>
  <!-- simple checkmark, css implementation can be done later -->
  <button class="selected" v-if="this.inbusket">✔ В корзине</button>
  <button v-else><slot></slot></button>
</template>

<script>
export default {
  props: {
    inbusket: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style scoped>
button {
  cursor: pointer;
  border: none;
  width: 122px;
  height: 48px;
  background-color: #403432;
  color: white;
  font-weight: 700;
  font-size: 14px;
  line-height: 21px;
  font-family: 'Merriweather', serif;
}

button:hover {
  background: #776763;
}

button:disabled {
  background: #c1b4b1;
}

.selected {
  background: #5b3a32;
}
</style>
