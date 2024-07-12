<template>
    <div class="chat-component">
      <h2>Conversación</h2>
      <div v-for="(mensaje, index) in mensajes" :key="index" class="conversacion-message" :style="{ backgroundColor: mensaje.color }">
        <p>
          <strong>{{ mensaje.sender }}:</strong> {{ mensaje.text }}
        </p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "ChatComponent",
    props: {
      mensajes: Array
    }
  };
  </script>
  
  <style scoped>
  .chat-component {
    width: 100%;
    margin-top: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  
  .conversacion-message {
    margin: 5px 0;
    padding: 5px;
  }
  </style>
  