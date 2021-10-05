<template>
  <button class="buy"><slot></slot></button>
</template>

<script>
export default {}
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
</style>
