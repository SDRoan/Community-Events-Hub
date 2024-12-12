<template>
  <div>
    <h2>Marketplace</h2>
    <Marketplaceform @add-item="addItem" /> 
    <ul>
      <li v-for="item in items" :key="item.id">
        <Marketplaceitem :item="item" />
      </li>
    </ul>
  </div>
</template>

<script>
import Marketplaceform from './components/Marketplaceform.vue';
import Marketplaceitem from './components/Marketplaceitem.vue';

export default {
  components: {
    Marketplaceform,
    Marketplaceitem
  },
  data() {
    return {
      items: [] 
    };
  },
  methods: {
    addItem(item) {
      
      this.items.push(item);
    }
  }
};
</script>
