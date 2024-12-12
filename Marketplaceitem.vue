<template>
  <div>
    <h4>{{ item.title }}</h4>
    <p>{{ item.description }}</p>
    <p>Price: ${{ item.price }}</p>
    <button v-if="!isSold" @click="buyItem(item.id)">Buy Item</button>
    <span v-else>Sold</span>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    },
    isSold: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    buyItem(itemId) {
      this.$emit('buy-item', itemId); 
    }
  }
};
</script>

<style scoped>
h4 {
  margin-bottom: 5px;
}

p {
  margin: 5px 0;
}

button {
  background-color: #28a745;
  color: white;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #218838;
}

span {
  color: grey;
}
</style>
