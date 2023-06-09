<template>
  <div v-if="modalEditOpen" class="modal">
    <FormComp typeData="edit" />
    <span @click="closeEditModal">Close edit modal</span>
  </div>
  <main class="users main-container">
    <h1>Usuários</h1>
    <ul>
      <li v-for="user in users" :key="user.name">
        <p>Nome: {{ user.name }}</p>
        <p>Idade: {{ user.age }}</p>
        <p>Email: {{ user.email }}</p>
        <button @click="openEditModal(user.name)">Editar</button>
        <button @click="openDeleteModal(user.name)">Deletar</button>
      </li>
    </ul>
    <p>páginas</p>
    <div>
      <button>&lt;</button>
      <p>{{ page }}</p>
      <button>></button>
    </div>
  </main>
</template>

<script>
import FormComp from "@/components/Form.vue";

export default {
  name: "UsersPage",
  components: {
    FormComp,
  },
  data() {
    return {
      users: [
        { id: 1, name: "Wesley", age: 22, email: "wesleydematos3@gmail.com" },
        { id: 2, name: "werbert", age: 22, email: "werbert@gmail.com" },
        { id: 3, name: "hortencia", age: 22, email: "hot3@gmail.com" },
      ],
      page: 1,
      nextPage: "link.com",
      modalEditOpen: false,
      modalDeleteOpen: false,
    };
  },
  methods: {
    openEditModal(name) {
      this.modalEditOpen = true;
      localStorage.setItem("username", name);
    },
    closeEditModal() {
      this.modalEditOpen = false;
    },
    openDeleteModal(name) {
      this.modalDeleteOpen = true;
      localStorage.setItem("username", name);
    },
    closeDeleteModal() {
      this.modalDeleteOpen = false;
    },
  },
};
</script>
