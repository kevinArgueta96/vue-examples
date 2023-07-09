<template>
  <v-app>
    <v-container>
      <v-form ref="form" v-model="valid">
        <v-text-field
          v-model="username"
          :rules="usernameRules"
          label="Nombre de usuario"
          required
        ></v-text-field>

        <v-text-field
          v-model="password"
          :rules="passwordRules"
          label="Contraseña"
          type="password"
          required
        ></v-text-field>

        <v-btn :disabled="!valid" @click="submit">Iniciar sesión</v-btn>

        <v-btn text @click="reset">Resetear</v-btn>
      </v-form>
    </v-container>
  </v-app>
</template>

<script>
import axios from '../axios';

export default {
  data: () => ({
    valid: true,
    username: '',
    usernameRules: [
      v => !!v || 'El nombre de usuario es requerido.',
    ],
    password: '',
    passwordRules: [
      v => !!v || 'La contraseña es requerida.',
    ],
  }),
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        
        axios.get('/api/games/list',  {
        // 
        withCredentials: true 
      })
      .then(response => {
        const data = response.data;
        console.log(data);
      })
      .catch(error => {
        console.error(error);
      });
        // Implementar la lógica de inicio de sesión aquí...
        console.log("Nombre de usuario: ", this.username);
        console.log("Contraseña: ", this.password);
      }
    },
    reset() {
      this.$refs.form.reset();
    },
  },
};
</script>
