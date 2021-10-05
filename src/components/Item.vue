<template>
  <div class="item" :class="{ opac: sold }">
    <img src="https://picsum.photos/280/160" alt="" class="item__image" />
    <h2 class="item__title">Lorem ipsum dolor</h2>
    <span v-if="sold" class="item__sold">Продана на аукционе</span>
    <div v-else class="item__wrapper">
      <div class="item-price-wrapper">
        <span class="item__price discount">20000$</span>
        <span class="item__price">10000$</span>
      </div>
      <base-button>Купить</base-button>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
h2 {
  margin: 0px;

  font-size: 18px;
  line-height: 27px;
}
.item__image {
  cursor: pointer;
}
.item-price-wrapper {
  display: flex;
  flex-direction: column;
}
.item__wrapper {
  display: flex;
  column-gap: 24px;
}

.item__price {
  font-weight: 700;
  font-size: 16px;
  line-height: 22px;
}

.discount {
  text-decoration: line-through;
  opacity: 0.5;
  font-weight: 300;
  font-size: 14px;
  line-height: 21px;
}

.item {
  width: 280px;
  border: 1px solid #e1e1e1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  padding-bottom: 24px;
}
</style>
