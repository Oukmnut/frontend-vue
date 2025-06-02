<template>
  <div>
    <h3>{{ editMode ? 'Edit' : 'Add' }} Product</h3>
    <form @submit.prevent="handleSubmit">
      <input v-model="form.name" class="form-control mb-2" placeholder="Name" required />
      <input v-model="form.price" class="form-control mb-2" placeholder="Price" type="number" required />
      <textarea v-model="form.description" class="form-control mb-2" placeholder="Description"></textarea>
      <button class="btn btn-primary">{{ editMode ? 'Update' : 'Create' }}</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['product', 'onSubmit'],
  data() {
    return {
      form: this.product || { name: '', price: '', description: '' },
      editMode: !!this.product
    }
  },
  watch: {
    product(newVal) {
      this.form = { ...newVal };
      this.editMode = !!newVal;
    }
  },
  methods: {
    handleSubmit() {
      this.onSubmit({ ...this.form });
      if (!this.editMode) this.form = { name: '', price: '', description: '' };
    }
  }
}
</script>
