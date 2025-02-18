<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <div v-for="product in inventory" :key="product.id" class="card">
        <ProductCard :product="product" :addToCart="addToCart" />
      </div>
    </div>
  </main>
</template>
<script>
import ProductCard from '@/components/ProductCard.vue'

export default {
  props: ['addToCart', 'inventory'],
  components: { ProductCard }
}
</script>
