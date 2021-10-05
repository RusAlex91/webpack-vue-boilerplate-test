<template>
  <div class="item-modal">
    <h2 class="item__title">Lorem ipsum dolor</h2>
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
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Sequi, eaque hic.
      Delectus, illo sed alias molestiae dolore voluptatibus explicabo
      consequuntur, soluta ullam facilis aut amet. Maxime esse hic provident
      neque.
    </p>
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
import SliderSlide from './ui/Slide.vue'
import Slider from './Slider.vue'
export default {
  data () {
    return {
      slides: [
        'https://picsum.photos/id/1000/560/320',
        'https://picsum.photos/id/1001/560/320',
        'https://picsum.photos/id/1002/560/320'
      ],
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
.item-modal__slider {
}
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

.item__desc {
  margin: 0px;
  padding: 0px;
  width: 500px;
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
