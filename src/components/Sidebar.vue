<script>
export default {
  props: ['toggle', 'cart', 'inventory', 'remove'],
  methods: {
    getPrice (id) {
      // eslint-disable-next-line eqeqeq
      const product = this.inventory.find(p => p.id == id) || 0
      return product.price.USD
    },
    getName (id) {
      // eslint-disable-next-line eqeqeq
      return this.inventory.find(p => p.id == id).name || 'Product Name Not Found'
    },
    calculateTotal () {
      return Object.entries(this.cart).reduce((acc, curr, index) =>
        acc + (curr[1] * this.getPrice(curr[0])), 0).toFixed(2)
    }
  }
}
</script>

<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
            <span>
              Cart
              <i class="icofont-cart-alt icofont-1x"></i>
            </span>
        <button @click="toggle" class="cart-close">&times;</button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(quantity, id) in cart" :key="id">
              <td><i class="icofont-carrot icofont-3x"></i></td>
              <td>{{ getName(id) }}</td>
              <td>{{ '$' + getPrice(id) }}</td>
              <td class="center">{{ quantity }}</td>
              <td> {{ '$' + quantity * getPrice(id) }}</td>
              <td class="center">
                <button class="btn btn-light cart-remove"
                        @click="remove(id)"
                >
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p class="center" v-if="!Object.keys(cart).length"><em>No items in cart</em></p>
        <div class="spread">
          <span><strong>Total:</strong> {{ '$' + calculateTotal() }}</span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>

<style scoped>

</style>
