<template>
  <div>
    <h3>Add a new item to the marketplace</h3>
    <form @submit.prevent="submitForm">
      <label for="title">Item Title:</label>
      <input type="text" v-model="item.title" id="title" required />
      
      <label for="description">Item Description:</label>
      <input type="text" v-model="item.description" id="description" required />
      
      <label for="price">Item Price:</label>
      <input type="number" v-model="item.price" id="price" disabled />
      
      <button type="submit">Add Item</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      item: {
        title: '',
        description: '',
        price: ''
      }
    };
  },
  methods: {
    submitForm() {
      this.$emit('add-item', this.item); // Emit the add-item event with the item data
      this.item = { title: '', description: '', price: '' }; // Clear the form fields after submission
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  margin-top: 20px;
}

label {
  margin-bottom: 5px;
}

input {
  margin-bottom: 15px;
  padding: 8px;
}

button {
  background-color: #007bff;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
