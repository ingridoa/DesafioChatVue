<template>
  <div id="app">
    <UsuarioComponent v-if="users.length" :user="users[0]" @enviarMensaje="handleEnviarMensaje($event, 0)"/>
    <UsuarioComponent v-if="users.length" :user="users[1]" @enviarMensaje="handleEnviarMensaje($event, 1)"/>
    <ChatComponent :mensajes="conversacion"/>
  </div>
</template>

<script>
import axios from "axios";
import UsuarioComponent from './components/UsuarioComponent.vue';
import ChatComponent from './components/ChatComponent.vue';

export default {
  name: 'App',
  components: {
    UsuarioComponent,
    ChatComponent
  },
  data() {
    return {
      users: [],
      conversacion: []
    };
  },
  async mounted() {
    try {
      const { data } = await axios.get('https://randomuser.me/api/?results=2');
      this.users = data.results;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    handleEnviarMensaje(mensaje, userIndex) {
      // Agregar el mensaje a la conversación
      this.conversacion.push(mensaje);

      // Simular respuesta del otro usuario
      const otroUserIndex = userIndex === 0 ? 1 : 0;
      const respuesta = {
        sender: this.users[otroUserIndex].name.first,
        text: `Respuesta a ${mensaje.text}`,
        color: '#ffffff' // color opcional para la respuesta
      };
      this.conversacion.push(respuesta);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: #333;
  margin-top: 20px;
}
</style>

