<template>
    <div class="event-card">
      <h3>{{ event.title }}</h3>
      <p>{{ event.description }}</p>
      <p><strong>Date:</strong> {{ event.date }}</p>
      <p><strong>Time:</strong> {{ event.time }}</p>
      <p><strong>Location:</strong> {{ event.location }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'EventCard',
    props: {
      event: Object
    }
  };
  </script>
  
  <style scoped>
  .event-card {
    border: 1px solid #ccc;
    padding: 20px;
    margin: 10px 0;
    border-radius: 5px;
    background-color: #f9f9f9;
  }
  .event-card h3 {
    margin-bottom: 10px;
  }
  </style>
  