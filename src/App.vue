<template>
  <div class="container my-5">
    <h3>AGREGAR USUARIOS</h3>
    <AgregaUsers />
    <hr class="my-5" />
    <h3>TABLA DE USUARIOS</h3>
    <MuestraUsers />
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
import firebaseApp from "./firebaseConfig.js";
import AgregaUsers from "./components/AgregaUsers.vue";
import MuestraUsers from "./components/MuestraUsers.vue";

export default {
  name: "App",
  components: {
    AgregaUsers,
    MuestraUsers,
  },
};
</script>

<style></style>
