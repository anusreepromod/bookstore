<template>
   <header class="top-bar spread">
        <nav class="top-bar-nav">
          <router-link to="/" class="top-bar-link">
            <i class="icofont"></i>
            <span>Home</span>
          </router-link>
          <router-link to="products" class="top-bar-link">
            <span>Books</span>
          </router-link>

        </nav>
        <div @click="toggleSidebar" class="top-bar-cart-link">
          <i class="icofont-cart-alt icofont-1x"></i>
          <span>Cart ({{totalQuantity}})</span>
        </div>
      </header>

  <router-view :inventory="inventory" :addToCart="addToCart"/>
  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />
</template>

<script>
import Sidebar from '@/components/SideBar.vue'
import food from './book.json'
export default {
  components: {
    Sidebar
  },
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      console.log(quantity)
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (name) {
      this.cart[name] -= 1
      if (this.cart[name] === 0) delete this.cart[name]
    }
  }
}
</script>
