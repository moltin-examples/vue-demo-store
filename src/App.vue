<template>
  <div class="ui text container" style="padding-top: 7em;">
    <div id="app">
      <div class="ui huge inverted top fixed menu">
        <div class="ui text container">
          <router-link to="/" class="header item">
            <img src="./assets/moltin-light-hex.svg" class="ui mini image" style="margin-right: 1.5em;">Vue.js Store
          </router-link>
          <router-link to="/cart" class="right item">
            Cart ({{ cart.data.length }} items)
          </router-link>
        </div>
      </div>
      <router-view :cart="cart" @cart-updated="onCartUpdated"></router-view>
    </div>
  </div>
</template>

<script>
import MoltinService from './services/moltin.js'

export default {
  name: 'app',
  data () {
    return {
      cart: {
        data: []
      }
    }
  },
  beforeMount () {
    MoltinService.getCart().then((response) => {
      this.cart = response
    })
  },
  methods: {
    onCartUpdated (cart) {
      this.cart = cart
    }
  }
}
</script>

<style>
  @import 'https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.2/semantic.min.css'
</style>
