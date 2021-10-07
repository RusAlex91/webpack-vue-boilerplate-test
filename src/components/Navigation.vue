<template>
  <nav>
    <!-- router-link instead a -->
    <ul>
      <li><a href="/catalog">Каталог</a></li>
      <li><a href="/delivery">Доставка</a></li>
      <li><a href="/payment">Оплата</a></li>
      <li><a href="/contacts">Контакты</a></li>
      <li><a href="/about">О компании</a></li>
    </ul>
  </nav>
</template>

<script>
export default {}
</script>

<style scoped>
ul {
  color: #343030;
  margin: 0;
  margin-top: 40px;
  margin-bottom: 40px;
  display: flex;
  column-gap: 48px;
}

li {
  padding: 0;
  margin: 5px;
  font-size: 14px;

  list-style: none;
}

li a {
  text-decoration: none;
  color: inherit;
  border: 1px solid transparent;
}

li:last-child {
  width: 13.333vw;
}

li a:hover {
  border: 1px solid #343030;
}

@media only screen and (max-width: 1080px) {
  ul {
    column-gap: 25px;
  }
}
@media only screen and (max-width: 870px) {
  li:last-child {
    width: 100px;
  }

  ul {
    margin-top: 20px;
    margin-bottom: 20px;
  }
}

@media only screen and (max-width: 510px) {
  ul {
    flex-direction: column;
    row-gap: 25px;
  }
  li:nth-child(2) {
    margin-left: 10px;
  }
  li:nth-child(4) {
    margin-left: 10px;
  }
  li:last-child {
    width: 100px;
  }
}
</style>
