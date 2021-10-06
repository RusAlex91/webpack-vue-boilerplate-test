<template>
  <div class="item" :class="{ paintSold: sold }">
    <img
      @click.stop="this.$emit('openmodal', true)"
      :src="preview"
      alt=""
      class="item__image"
    />
    <h2 class="item__title">"{{ name }}"</h2>
    <span v-if="sold" class="item__sold">Продана на аукционе</span>
    <div v-else class="item__wrapper">
      <div class="item-price-wrapper">
        <span class="item__price discount">{{ newPrice }}$</span>
        <span class="item__price">{{ price }}$</span>
      </div>

      <base-button @click="addtoCart" :inbusket="selected">{{
        btnText
      }}</base-button>
      <span v-show="preload" class="preloader">
        <div class="clock-loader"></div>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      selected: false,
      preload: false,
      btnText: 'Купить'
    }
  },
  props: {
    id: {
      type: Number,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    preview: {
      type: String,
      required: false
    },
    images: {
      type: Array,
      required: false
    },
    price: {
      type: Number,
      required: false
    },
    newPrice: {
      type: Number,
      required: false
    },
    sold: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    addtoCart () {
      this.preload = true
      this.btnText = ' '
      setTimeout(() => {
        this.preload = false
        this.selected = !this.selected
        if (this.selected) {
          this.btnText = '✔ В корзине'
          localStorage.setItem(this.id, true)
        } else if (!this.selected) {
          this.btnText = 'Купить'
          localStorage.removeItem(this.id)
        }
      }, 1000)
    }
  },
  mounted () {
    const key = localStorage.key(this.id)
    if (key) {
      this.selected = true
      this.btnText = '✔ В корзине'
    }
  }
}
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
  position: relative;
}

.item__sold {
  margin-top: 20px;
}

.paintSold {
  opacity: 0.5;
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

.preloader {
  position: absolute;
  top: 10px;
  left: 145px;
}

.clock-loader {
  width: 25px;
  height: 25px;
  background-color: rgb(129, 129, 129);
  border-radius: 30px;
  position: relative;
}
.clock-loader::after {
  width: 5px;
  height: 5px;
  background-color: white;
  border-radius: 20px;
  top: 10px;
  left: 10px;
  position: absolute;
  content: '';
  animation: round 0.5s infinite reverse;
}

@keyframes round {
  from {
    transform: rotate(0deg) translateX(10px) rotate(0deg);
  }
  to {
    transform: rotate(360deg) translateX(10px) rotate(-360deg);
  }
}
</style>
