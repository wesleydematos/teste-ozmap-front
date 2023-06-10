<template>
  <div v-if="modalEditOpen" class="modal">
    <FormComp typeData="edit" :functionProp="closeEditModal" />
    <span @click="closeEditModal">Close edit modal</span>
  </div>
  <div v-if="modalDeleteOpen" class="modal">
    <div>Tem certeza que deseja deletar usuário?</div>
    <div>
      <button @click="deleteUser">Sim</button>
      <button @click="closeDeleteModal">Cancelar</button>
    </div>
    <span @click="closeDeleteModal">Close delete modal</span>
  </div>
  <main class="users main-container">
    <h1>Usuários:</h1>
    <div class="pages">
      <p>Páginas:</p>
      <button :disabled="page == 1" @click="getLastPage">&lt;</button>
      <p>{{ page }}</p>
      <button :disabled="page >= totalPage" @click="getNextPage">></button>
    </div>
    <ul>
      <li v-for="user in users" :key="user.name">
        <p>Nome: {{ user.name }}</p>
        <p>Idade: {{ user.age }}</p>
        <p>Email: {{ user.email }}</p>
        <button @click="openEditModal(user.name)">Editar</button>
        <button @click="openDeleteModal(user.name)">Deletar</button>
      </li>
    </ul>
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
      users: [],
      page: 1,
      totalPage: 0,
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
      this.getUsers();
    },

    openDeleteModal(name) {
      this.modalDeleteOpen = true;
      localStorage.setItem("username", name);
    },

    closeDeleteModal() {
      this.modalDeleteOpen = false;
    },

    async getUsers() {
      const req = await fetch(`http://localhost:3000/users/?page=${this.page}`);

      const data = await req.json();

      const totalPage = Math.ceil(data.total / 10);
      this.totalPage = totalPage;

      this.users = data.rows;
      this.nextPage = data.nextPage;
    },

    async deleteUser() {
      const username = localStorage.getItem("username");

      await fetch(`http://localhost:3000/user/${username}`, {
        method: "DELETE",
      });

      this.getUsers();
      this.closeDeleteModal();
    },

    getNextPage() {
      this.page += 1;
      this.getUsers();
    },

    getLastPage() {
      this.page -= 1;
      this.getUsers();
    },
  },
  mounted() {
    this.getUsers();
  },
};
</script>

<style scoped>
.users {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  margin: 2rem 0;
}

ul {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  max-width: 80%;
  gap: 3rem;
}

li {
  width: 280px;
}

.pages {
  margin-bottom: 3.5rem;
  display: flex;
  gap: 0.3rem;
}
</style>
