<template>
  <div class="home main-container">
    <div>
      <h1>Cadastre usuários:</h1>
    </div>
    <FormComp typeData="create" />
  </div>
</template>

<script>
import FormComp from "@/components/Form.vue";

export default {
  name: "RegisterPage",
  components: {
    FormComp,
  },
};
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
}

div {
  margin: 2rem 0;
}
</style>
