<template>
  <div>
    <product-form :product="editProduct" :onSubmit="saveProduct" />

    <table class="table table-bordered mt-4">
      <thead>
        <tr>
          <th>Name</th><th>Price</th><th>Description</th><th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product._id">
          <td>{{ product.name }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.description }}</td>
          <td>
            <button class="btn btn-warning btn-sm" @click="editProduct = product">Edit</button>
            <button class="btn btn-danger btn-sm" @click="deleteProduct(product._id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
import ProductForm from './ProductForm.vue';

export default {
  components: { ProductForm },
  data() {
    return {
      products: [],
      editProduct: null
    }
  },
  methods: {
    async fetchProducts() {
      const res = await axios.get('http://localhost:5000/api/products');
      this.products = res.data;
    },
    async saveProduct(product) {
      if (product._id) {
        await axios.put(`http://localhost:5000/api/products/${product._id}`, product);
      } else {
        await axios.post('http://localhost:5000/api/products', product);
      }
      this.editProduct = null;
      this.fetchProducts();
    },
    async deleteProduct(id) {
      await axios.delete(`http://localhost:5000/api/products/${id}`);
      this.fetchProducts();
    }
  },
  mounted() {
    this.fetchProducts();
  }
}
</script>
