<template>
  <header>
    <div class="logo">
      <p>OzUsers</p>
    </div>
    <nav>
      <a>Cadastro</a>
      <a>Usuários</a>
    </nav>
  </header>
</template>

<script>
export default {
  name: "HeaderComp",
};
</script>

<style scoped>
header {
  display: flex;
  background-color: #131313;
  height: 5rem;
  justify-content: space-around;
  align-items: center;
}

.logo > p {
  font-size: 2rem;
}

nav {
  display: flex;
  gap: 0.8rem;
}

nav > a {
  font-size: 1.5rem;
}
</style>
