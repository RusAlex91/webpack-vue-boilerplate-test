<template>
  <div class="item-modal">
    <h2 class="item__title">{{ name }}</h2>
    <slider
      @next="slider('next')"
      @prev="slider('prev')"
      class="item-modal__slider"
    >
      <slider-slide
        v-for="(slide, index) in slides"
        :key="slide"
        :index="index"
        :visibleSlide="visibleSlide"
        :direction="direction"
      >
        <img :src="slide" alt="" />
      </slider-slide>
    </slider>

    <p class="item__desc">
      {{ desc }}
    </p>
    <span v-if="sold" class="item__sold">Продана на аукционе</span>
    <div v-else class="item__wrapper">
      <div class="item-price-wrapper">
        <span class="item__price discount">{{ newPrice }}$</span>
        <span class="item__price">{{ price }}$</span>
      </div>
      <base-button>Купить</base-button>
    </div>
  </div>
</template>

<script>
import SliderSlide from './ui/Slide.vue'
import Slider from './Slider.vue'
export default {
  props: {
    name: {
      type: String,
      required: true
    },
    images: {
      type: Array,
      required: false
    },
    desc: {
      type: String,
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
  data () {
    return {
      slides: [],
      visibleSlide: 0,
      direction: 'left'
    }
  },
  computed: {
    slideLen () {
      return this.slides.length
    }
  },
  methods: {
    slider (action) {
      if (action === 'next') {
        if (this.visibleSlide >= this.slideLen - 1) {
          this.visibleSlide = 0
        } else {
          this.visibleSlide++
        }
        this.direction = 'left'
      } else {
        if (this.visibleSlide <= 0) {
          this.visibleSlide = this.slideLen - 1
        } else {
          this.visibleSlide--
        }
        this.direction = 'right'
      }
    }
  },
  components: {
    SliderSlide,
    Slider
  },
  mounted () {
    this.slides = this.images
  }
}
</script>

<style scoped>
.item-modal {
  border: 1px solid #e1e1e1;
  padding: 10px;
  background-color: #eceaea;
  position: fixed;
  top: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 560px;
  row-gap: 20px;
}

h2 {
  margin: 0px;
  margin-top: 10px;
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

.item__desc {
  margin: 0px;
  padding: 0px;
  width: 500px;
  height: 100px;
  text-align: justify;
}

.item__sold {
  align-items: center;
  justify-content: center;
  display: flex;
  background-color: lightgray;
  border: 1px solid gray;
  height: 30px;
  width: 100%;
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

.item-modal__slider-controls button {
  border: none;
  background-color: transparent;
  cursor: pointer;
}
</style>
