<template>
    <div class="event-card">
      <h3>{{ event.title }}</h3>
      <p>{{ event.description }}</p>
      <p>Date: {{ event.date }}</p>
      <p>Time: {{ event.time }}</p>
      <p>Location: {{ event.location }}</p>
      <button>RSVP</button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['event'],
  };
  </script>