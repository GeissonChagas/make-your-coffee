<template>
    <div class="message-container">
      <p>{{ msg }}</p>
    </div>
  </template>
  
  <script>
    export default {
      name: "Message",
      props: {
        msg: String
      }
    }
  </script>
  
  <style scoped>
    .message-container {
      color: #008543;
      background-color: #8de9c3;
      border: 2px solid #8ff3d2;
      border-radius: 5px;
      padding: 10px;
      max-width: 400px;
      margin: 30px auto;
    }
  </style>