<template>
  <div v-if="modalEditOpen" class="modal">
    <FormComp typeData="edit" />
    <span @click="closeEditModal">Close edit modal</span>
  </div>
  <main>
    <h1>Usuários</h1>
    <ul>
      <li v-for="user in users" :key="user.name">
        <p>Nome: {{ user.name }}</p>
        <p>Idade: {{ user.age }}</p>
        <p>Email: {{ user.email }}</p>
        <button @click="openEditModal">Edit</button>
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
    };
  },
  methods: {
    openEditModal() {
      this.modalEditOpen = true;
    },
    closeEditModal() {
      this.modalEditOpen = false;
    },
  },
};
</script>
