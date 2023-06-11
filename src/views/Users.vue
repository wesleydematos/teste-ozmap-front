<template>
  <div v-if="modalEditOpen" class="modal">
    <div class="contentModal">
      <span @click="closeEditModal">X</span>
      <h1>Editar usuário:</h1>
      <FormComp typeData="edit" :functionProp="closeEditModal" />
    </div>
  </div>
  <div v-if="modalDeleteOpen" class="modal">
    <div class="contentModal">
      <span @click="closeDeleteModal">X</span>
      <div>Tem certeza que deseja deletar o usuário {{ user }}?</div>
      <div class="btns">
        <button @click="deleteUser">Sim</button>
        <button @click="closeDeleteModal" class="cancel">Cancelar</button>
      </div>
      <MessageComp :msg="msg" v-show="msg" />
    </div>
  </div>
  <main class="users main-container">
    <h1>Usuários:</h1>
    <div class="pages">
      <p>Páginas:</p>
      <button :disabled="page == 1" @click="getLastPage">&lt;</button>
      <p>{{ page }} de {{ totalPage }}</p>
      <button :disabled="page >= totalPage" @click="getNextPage">></button>
    </div>
    <ul>
      <li v-for="user in users" :key="user.name">
        <p>Nome: {{ user.name }}</p>
        <p>Idade: {{ user.age }}</p>
        <p>Email: {{ user.email }}</p>
        <div class="btns">
          <button @click="openEditModal(user.name)">Editar</button>
          <button @click="openDeleteModal(user.name)">Deletar</button>
        </div>
      </li>
    </ul>
  </main>
</template>

<script>
import FormComp from "@/components/Form.vue";
import MessageComp from "@/components/Message.vue";

export default {
  name: "UsersPage",
  components: {
    FormComp,
    MessageComp,
  },
  data() {
    return {
      msg: null,
      user: "",
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
      this.user = name;
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

      const response = await fetch(`http://localhost:3000/user/${username}`, {
        method: "DELETE",
      });

      console.log(response);
      if (response.status == 204) {
        this.msg = "Usuário deletado com sucesso!";
      } else {
        this.msg = "Não foi possível deletar o usuário!";
      }
      setTimeout(() => (this.msg = ""), 1500);
      setTimeout(() => this.closeDeleteModal(), 1500);
      this.getUsers();
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
.modal {
  display: flex;
  justify-content: center;
  position: fixed;
  z-index: 1000;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.9);
}

.contentModal {
  color: black;
  display: flex;
  flex-direction: column;
  background: #1d1d1d;
  margin-top: 5rem;
  min-height: 150px;
  border-radius: 10px;
  padding: 10px;
  height: fit-content;
}

.contentModal > h1,
div {
  color: #ffff;
}

.contentModal > div {
  font-size: large;
  margin: 9px 0;
}

.contentModal > span {
  color: red;
  align-self: flex-end;
  cursor: pointer;
  font-size: larger;
}

.users {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  margin: 2rem 0;
}

.pages {
  margin-bottom: 3.5rem;
  display: flex;
  gap: 0.3rem;
}

button {
  color: #ffff;
  border: none;
  border-radius: 5px;
  background-color: #00d256;
  font-size: large;
}

button:hover {
  background-color: #003e1a;
}
.pages > button {
  width: 20px;
  height: 20px;
}

.pages > button:disabled {
  background-color: #134d2b;
  cursor: not-allowed;
}

ul {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  max-width: 80%;
  gap: 3rem;
}

li {
  border: 2px solid #00d256;
  border-top: 5px solid #00d256;
  border-radius: 8px;
  background-color: #ffff;
  color: #000;
  width: 300px;
  height: 130px;
  padding: 7px;
  overflow: hidden;
  font-size: larger;
}

li > p {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}

.btns {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 10px;
}

.btns > button {
  height: 25px;
  min-width: 65px;
}
.cancel {
  background-color: red;
  width: 80px;
}

.cancel:hover {
  background-color: rgb(165, 0, 0);
}
</style>
