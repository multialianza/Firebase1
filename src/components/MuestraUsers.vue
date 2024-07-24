<template>
  <table class="table">
    <thead>
      <tr>
        <th scope="col">ID</th>
        <th scope="col">NOMBRE</th>
        <th scope="col">EMAIL</th>
        <th scope="col">ELIMINAR</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="usuario in usuarios" :key="usuario.id">
        <th scope="row">{{ usuario.id }}</th>
        <td>{{ usuario.nombre }}</td>
        <td>{{ usuario.email }}</td>
        <td>
          <button class="btn btn-danger" @click="deleteUsuario(usuario.id)">
            X
          </button>
        </td>
      </tr>
    </tbody>
  </table>
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
  name: "MuestraUsers",
  data() {
    return {
      usuarios: [],
    };
  },
  mounted() {
    const db = getFirestore(firebaseApp);
    const usuarioRef = collection(db, "usuarios");
    onSnapshot(usuarioRef, (snapshot) => {
      this.usuarios = snapshot.docs.map((doc) => ({
        id: doc.id,
        ...doc.data(),
      }));
    });
  },
  methods: {
    async deleteUsuario(usuarioId) {
      const db = getFirestore(firebaseApp);
      const usuarioRef = doc(db, "usuarios", usuarioId);
      await deleteDoc(usuarioRef);
    },
  },
};
</script>

<style scoped></style>
