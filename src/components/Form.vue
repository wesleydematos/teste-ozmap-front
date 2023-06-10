<template>
  <form @submit="sendData($event)">
    <div>
      <label for="name">Nome<span>*</span></label>
      <input type="text" v-model="name" id="name" />
    </div>
    <div>
      <label for="email">Email<span>*</span></label>
      <input type="email" v-model="email" id="email" />
    </div>
    <div>
      <label for="age">Idade<span>*</span></label>
      <input type="number" min="18" v-model="age" id="age" />
    </div>
    <button>Enviar</button>
  </form>
  <MessageComp :msg="msg" v-show="msg" />
</template>

<script>
import MessageComp from "@/components/Message.vue";

export default {
  name: "FormComp",
  components: {
    MessageComp,
  },
  props: {
    typeData: String,
    functionProp: Promise,
  },
  data() {
    return {
      name: "",
      email: "",
      age: "",
      msg: null,
    };
  },
  mounted() {
    if (this.typeData == "edit") {
      this.getUserData();
    }
  },
  methods: {
    async sendData(e) {
      e.preventDefault();

      const data = { name: this.name, email: this.email, age: this.age };
      const dataJson = JSON.stringify(data);

      if (this.typeData == "create") {
        const response = await fetch("http://localhost:3000/user", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: dataJson,
        });

        if (response.status == 201) {
          this.msg = "Usuário criado com sucesso!";

          setTimeout(() => (this.msg = ""), 3000);
        } else {
          response.status == 409
            ? (this.msg = "Usuário com este nome já foi cadastrado!")
            : (this.msg = "Não foi possível criar usuário!");

          setTimeout(() => (this.msg = ""), 3000);
        }
      }

      if (this.typeData == "edit") {
        const username = localStorage.getItem("username");

        const response = await fetch(`http://localhost:3000/user/${username}`, {
          method: "PATCH",
          headers: { "Content-Type": "application/json" },
          body: dataJson,
        });

        if (response.status == 200) {
          this.msg = "Usuário editado com sucesso!";

          setTimeout(() => (this.msg = ""), 3000);
        } else {
          response.status == 409
            ? (this.msg = "Usuário com este nome já foi cadastrado!")
            : (this.msg = "Não foi possível editar usuário!");

          setTimeout(() => (this.msg = ""), 3000);
        }
      }
      setTimeout(() => this.functionProp(), 2000);

      this.name = "";
      this.email = "";
      this.age = "";
    },

    async getUserData() {
      const username = localStorage.getItem("username");

      const req = await fetch(`http://localhost:3000/user/${username}`);

      const user = await req.json();

      this.name = user.name;
      this.email = user.email;
      this.age = user.age;
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  width: 80vw;
}

div {
  display: flex;
  flex-direction: column;
}

label {
  color: #00d256;
  font-size: larger;
}

input {
  border-radius: 5px;
  font-size: larger;
  padding: 0 5px;
}

input,
button {
  height: 30px;
  border: none;
}

span {
  color: red;
}

button {
  border-radius: 20px;
  width: 50%;
  margin-top: 0.3rem;
  align-self: center;
  background-color: #00d256;
  color: #ffff;
  font-size: large;
}

@media (min-width: 1024px) {
  form {
    width: 60vw;
  }

  input,
  button {
    height: 50px;
  }
}
</style>
