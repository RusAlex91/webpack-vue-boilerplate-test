<template>
  <form>
    <label for="search"></label>
    <input
      placeholder="Поиск по названию картины"
      type="search"
      id="search"
      name="search"
    />
    <base-button>Найти</base-button>
  </form>
</template>

<script>
export default {}
</script>

<style scoped>
form {
  margin: 0;
  display: flex;
}

input {
  width: 420px;
  height: 48px;
  border: 1px solid #e1e1e1;
  background: #f6f3f3;
  font-family: 'Merriweather', serif;
}

input:focus {
  outline: none;
  border: 1px solid #9c9c9c;
  border-radius: 0px;
}

input[type='search']::placeholder {
  padding: 15px;
  opacity: 0.8;
}

@media only screen and (max-width: 1200px) {
  input {
    width: 250px;
  }
}

@media only screen and (max-width: 1330px) {
  input {
    width: 250px;
  }
}
@media only screen and (max-width: 936px) {
  input {
    width: 240px;
  }
}
@media only screen and (max-width: 360px) {
  input {
    width: 140px;
  }
  input[type='search']::placeholder {
    padding: 5px;
    opacity: 0.8;
  }
}
</style>
