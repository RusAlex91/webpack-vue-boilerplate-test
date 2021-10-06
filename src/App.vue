<template>
  <div class="app-wrapper" @click.self="disableModal">
    <header>
      <navigation-component></navigation-component>
      <search></search>
    </header>
    <main @click.self="disableModal">
      <!-- <router-view></router-view> -->
      <div class="main-items" @click.self="disableModal">
        <h1>Картины эпохи Lorem</h1>
        <div class="items" @click.self="disableModal">
          <item
            v-for="painting in items"
            :key="painting.id"
            :id="painting.id"
            :name="painting.name"
            :preview="painting.preview"
            :images="painting.images"
            :price="painting.price"
            :newPrice="painting.newPrice"
            :sold="painting.sold"
            v-on:openmodal="openModal(painting.id)"
          ></item>
        </div>
      </div>
      <span v-show="modalLoading" class="preloader">
        <div class="clock-loader"></div>
      </span>
      <transition name="smooth">
        <modal-item
          :name="modalItem.name"
          :images="modalItem.images"
          :desc="modalItem.description"
          :price="modalItem.price"
          :newPrice="modalItem.newPrice"
          :sold="modalItem.sold"
          v-show="modal"
          v-on:imgload="modalReady"
        ></modal-item>
      </transition>
    </main>
    <footer>
      <footer-component></footer-component>
    </footer>
  </div>
</template>

<script>
import FooterComponent from './components/Footer.vue'
import Item from './components/Item.vue'
import NavigationComponent from './components/Navigation.vue'
import ModalItem from './components/ModalItem.vue'
import Search from './components/Search.vue'

export default {
  data () {
    return {
      modal: false,
      items: null,
      modalId: null,
      modalItem: {},
      modalLoad: false,
      modalLoading: false
    }
  },
  methods: {
    openModal (id) {
      if (id == this.modalId) {
        this.modal = true
      }
      this.items.find(obj => {
        if (obj.id === id) {
          this.modalItem = obj
          this.modalLoading = true
          this.modalId = id
        }
      })
    },
    disableModal () {
      console.log('disable')
      if (this.modal) {
        this.modal = false
        this.modalLoad = false
        this.modalLoading = false
      }
    },
    modalReady () {
      console.log('modal ready')
      this.modal = true
    }
  },
  components: { FooterComponent, Item, NavigationComponent, ModalItem, Search },

  mounted () {
    fetch(
      'https://my-json-server.typicode.com/RusAlex91/webpack-vue-boilerplate-test/paintings'
    )
      .then(response => response.json())
      .then(paintings => (this.items = paintings))
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Merriweather:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&display=swap');

.app-wrapper {
  height: 100%;
}

body {
  background: #f6f3f3;
  font-family: 'Merriweather', serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  column-gap: 180px;
  border-bottom: 1px solid #e1e1e1;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  font-size: 24px;
  font-weight: bold;
  margin-top: 45px;
  margin-bottom: 40px;
}

.items {
  display: flex;
  column-gap: 32px;
  row-gap: 32px;
  width: 1250px;
  flex-wrap: wrap;
}

footer {
  width: 100%;
  position: fixed;
  bottom: 0;
}

.smooth-enter-active {
  animation: opacity 0.1s ease-in;
}
.smooth-leave-active {
  animation: opacity 0.1s reverse ease;
}
@keyframes opacity {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

.clock-loader {
  width: 50px;
  height: 50px;
  background-color: rgb(78, 78, 78);
  border-radius: 30px;
  position: relative;
}
.clock-loader::after {
  width: 10px;
  height: 10px;
  background-color: white;
  border-radius: 20px;
  top: 20px;
  left: 20px;
  position: absolute;
  content: '';
  animation: round 0.5s infinite reverse;
}

@keyframes round {
  from {
    transform: rotate(0deg) translateX(20px) rotate(0deg);
  }
  to {
    transform: rotate(360deg) translateX(20px) rotate(-360deg);
  }
}
</style>
