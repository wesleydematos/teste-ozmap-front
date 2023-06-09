<template>
  <form @submit="sendData($event)">
    <input type="text" v-model="name" id="name" />
    <input type="email" v-model="email" id="email" />
    <input type="number" min="18" v-model="age" id="age" />
    <button>enviar</button>
  </form>
</template>

<script>
export default {
  name: "FormComp",
  props: {
    typeData: String,
  },
  data() {
    return {
      name: "",
      email: "",
      age: "",
    };
  },
  methods: {
    sendData(e) {
      e.preventDefault();

      //se for == edit
      //seta os campos atraves de uma requisicao de buscar dados
      console.log({ name: this.name, email: this.email, age: this.age });
      //manda os campos pra requisicao de patch

      //se for == create
      //conferir se todos os campos estão sendo enviados
      //manda os campos para requisiçao de post

      alert(this.typeData);

      this.name = "";
      this.email = "";
      this.age = "";
    },
  },
};
</script>
