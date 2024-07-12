<template>
  <div class="usuario-chat">
    <img :src="user.picture.large" alt="">
    <p>{{ user.name.first }} {{ user.name.last }}</p>

    <form @submit.prevent="enviarMensaje">
      <div class="form-group">
        <label for="color">Color Chat:</label>
        <input type="color" v-model="color" id="color" />
      </div>
      <div class="form-group">
        <label for="message">Mensaje:</label>
        <textarea v-model="mensaje" id="message"></textarea>
      </div>
      <button type="submit">Enviar</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "UsuarioComponent",
  props: {
    user: Object,
  },
  data() {
    return {
      color: "#000000",
      mensaje: "",
    };
  },
  methods: {
    enviarMensaje() {
      // Emitir evento con el mensaje, el usuario y el color
      this.$emit("enviarMensaje", {
        sender: this.user.name.first,
        text: this.mensaje,
        color: this.color,
      });
      // Limpiar campos después de enviar
      this.mensaje = "";
      this.color = "#000000";
    },
  },
};
</script>

<style>
.usuario-chat {
  display: flex;
  align-items: flex-start;
}

.user-image {
  margin-right: 20px;
  border-radius: 50%;
}

.user-info {
  flex: 1;
}

.form-group {
  margin-bottom: 10px;
}

form {
  display: flex;
  flex-direction: column;
}

button {
  align-self: flex-start;
}
</style>
