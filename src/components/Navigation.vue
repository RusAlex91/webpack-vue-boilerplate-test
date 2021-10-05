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
  margin: 0;
  font-size: 14px;
  list-style: none;
}

li a {
  text-decoration: none;
  color: inherit;
}
</style>
