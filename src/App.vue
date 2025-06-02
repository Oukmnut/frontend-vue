<template>
  <div class="container mt-5">
    <h1 class="mb-4">Vue + Node CRUD App</h1>
    <product-list />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';

export default {
  components: { ProductList }
}
</script>
