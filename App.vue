<template>
  <div id="app">
    <h1>Community Events Hub</h1>

    
    <section>
      <h2>Upcoming Events</h2>
      <div v-for="event in events" :key="event.id">
        <EventCard :event="event" />
      </div>
    </section>

   
    <section>
      <h2>Marketplace</h2>
      <Marketplaceform @add-item="addItem" />
      
      <h3>Wallet: ${{ wallet }}</h3> 

      <h3>Available Items</h3>
      <ul>
        <li v-for="item in items" :key="item.id">
          <Marketplaceitem :item="item" @buy-item="showCardModal" />
        </li>
      </ul>

      <h3>Bought Items</h3>
      <ul>
        <li v-for="item in boughtItems" :key="item.id">
          <Marketplaceitem :item="item" :isSold="true" />
        </li>
      </ul>
    </section>

    <!-- Credit Card Modal -->
    <div v-if="showCardForm" class="modal">
      <div class="modal-content">
        <span class="close" @click="closeCardModal">&times;</span>
        <h3>Enter your Credit/Debit Card Information</h3>
        <form @submit.prevent="processTransaction">
          <div>
            <label for="cardNumber">Card Number:</label>
            <input type="text" v-model="cardInfo.cardNumber" maxlength="16" placeholder="Enter 16 digit card number" required />
          </div>
          <div>
            <label for="nameOnCard">Name on Card:</label>
            <input type="text" v-model="cardInfo.nameOnCard" placeholder="John Doe" required />
          </div>
          <div>
            <label for="expirationDate">Expiration Date (MM/YY):</label>
            <input type="text" v-model="cardInfo.expirationDate" placeholder="MM/YY" required />
          </div>
          <div>
            <label for="cvv">Security Code (CVV):</label>
            <input type="text" v-model="cardInfo.cvv" maxlength="3" placeholder="123" required />
          </div>
          <button type="submit">Submit Payment</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import EventCard from './components/EventCard.vue';
import Marketplaceform from './components/Marketplaceform.vue';
import Marketplaceitem from './components/Marketplaceitem.vue';

export default {
  name: 'App',
  components: {
    EventCard,
    Marketplaceform,
    Marketplaceitem
  },
  data() {
    return {
      events: [
        { id: 1, title: 'Yoga at the Park', description: 'A relaxing yoga session.', date: '2024-12-20', time: '10:00 AM', location: 'City Park' },
        { id: 2, title: 'Community Cleanup', description: 'Help clean the park.', date: '2024-12-21', time: '9:00 AM', location: 'Greenway Park' }
      ],
      items: [],
      boughtItems: [],
      wallet: 300,
      showCardForm: false,  
      selectedItem: null,   
      cardInfo: {
        cardNumber: '',
        nameOnCard: '',
        expirationDate: '',
        cvv: ''
      }
    };
  },
  methods: {
    addItem(newItem) {
      const randomPrice = (Math.random() * 30).toFixed(2);
      newItem.price = randomPrice;
      this.items.push(newItem);
    },
    showCardModal(itemId) {
      this.selectedItem = this.items.find(item => item.id === itemId);
      this.showCardForm = true;
    },
    closeCardModal() {
      this.showCardForm = false;
      this.resetCardInfo();
    },
    processTransaction() {
      const { cardNumber, nameOnCard, expirationDate, cvv } = this.cardInfo;

      // Validate card details (mock validation)
      if (cardNumber.length === 16 && nameOnCard && expirationDate && cvv.length === 3) {
        if (this.wallet >= this.selectedItem.price) {
          this.wallet = (this.wallet - this.selectedItem.price).toFixed(2);
          this.boughtItems.push(this.selectedItem);
          this.items = this.items.filter(item => item.id !== this.selectedItem.id); 
          alert('Transaction successful! You bought ' + this.selectedItem.title);
          this.closeCardModal();
        } else {
          alert('Not enough funds in wallet!');
        }
      } else {
        alert('Please fill out all fields correctly!');
      }
    },
    resetCardInfo() {
      this.cardInfo = {
        cardNumber: '',
        nameOnCard: '',
        expirationDate: '',
        cvv: ''
      };
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}

h1 {
  font-size: 3em;
}

section {
  margin: 20px 0;
}

h2 {
  font-size: 1.5em;
}

button {
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #28a745;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #218838;
}

h3 {
  font-size: 1.2em;
  color: #2c3e50;
  margin-top: 10px;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  width: 300px;
}

input {
  margin-bottom: 10px;
  padding: 8px;
  width: 100%;
  border-radius: 4px;
  border: 1px solid #ccc;
}

button[type="submit"] {
  background-color: #28a745;
  color: white;
  border: none;
  padding: 10px 20px;
  width: 100%;
}

button[type="submit"]:hover {
  background-color: #218838;
}

.close {
  position: absolute;
  top: 5px;
  right: 5px;
  font-size: 1.5em;
  cursor: pointer;
}
</style>
