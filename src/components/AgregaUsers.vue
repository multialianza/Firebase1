<template>
  <div>
    <form @submit.prevent="addUsuario" class="my-4">
      <label for="nombre" class="form-label">Nombre</label>
      <input
        v-model="this.$store.state.nuevoUsuario"
        placeholder="Nombre del Usuario"
        type="text"
        name="nombre"
        required
        class="form-control"
      />
      <label for="correo" class="form-label mt-3">Email</label>
      <input
        v-model="this.$store.state.nuevoCorreo"
        placeholder="Email del usuario"
        type="email"
        name="correo"
        required
        class="form-control"
      />
      <button type="submit" class="btn btn-primary mt-3">Agregar</button>
    </form>
  </div>
</template>

<script>
import {
  getFirestore,
  collection,
  onSnapshot,
  addDoc,
  doc,
  deleteDoc,
} from "firebase/firestore";
import firebaseApp from "../firebaseConfig.js";
export default {
  name: "AgregaUsers",
  methods: {
    async addUsuario() {
      const db = getFirestore(firebaseApp);
      const usuarioRef = collection(db, "usuarios");
      await addDoc(usuarioRef, {
        nombre: this.$store.state.nuevoUsuario,
        email: this.$store.state.nuevoCorreo,
      });
      this.$store.state.nuevoUsuario = "";
      this.$store.state.nuevoCorreo = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
