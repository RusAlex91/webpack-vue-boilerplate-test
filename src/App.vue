<template>
  <header>
    <navigation-component></navigation-component>
    <search></search>
  </header>
  <main @click.stop="">
    <!-- <router-view></router-view> -->
    <div class="main-items">
      <h1>Картины эпохи Lorem</h1>
      <div class="items">
        <item
          v-for="painting in items"
          :key="painting.id"
          :name="painting.name"
          :preview="painting.preview"
          :images="painting.images"
          :price="painting.price"
          :newPrice="painting.newPrice"
          :sold="painting.sold"
          @click.stop="openModal(painting.id)"
        ></item>
      </div>
    </div>
    <modal-item
      :name="modalItem.name"
      :images="modalItem.images"
      :desc="modalItem.description"
      :price="modalItem.price"
      :newPrice="modalItem.newPrice"
      :sold="modalItem.sold"
      v-if="modal"
    ></modal-item>
  </main>
  <footer>
    <footer-component></footer-component>
  </footer>
</template>

<script>
import FooterComponent from './components/Footer.vue'
import Item from './components/Item.vue'
import NavigationComponent from './components/Navigation.vue'
import ModalItem from './components/ModalItem.vue'
import Search from './components/Search.vue'

import { ref } from 'vue'
export default {
  data () {
    return {
      modal: false,
      items: null,
      modalItem: null
    }
  },
  methods: {
    openModal (id) {
      this.items.find(obj => {
        if (obj.id === id) {
          this.modalItem = obj
          this.modal = !this.modal
        }
      })
    },
    disableModal () {
      if (this.modal) {
        this.modal = false
      }
    }
  },
  components: { FooterComponent, Item, NavigationComponent, ModalItem, Search },
  setup () {
    const count = ref(0)
    const inc = () => {
      count.value++
    }
    return {
      count,
      inc
    }
  },
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
</style>
