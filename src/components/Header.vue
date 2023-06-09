<template>
  <header>
    <div class="logo">
      <p>OzUsers</p>
    </div>
    <nav>
      <router-link to="/">Cadastro</router-link>
      <router-link to="/users">Usuários</router-link>
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
  font-size: 1.8rem;
}

nav {
  display: flex;
  gap: 0.8rem;
}

a {
  font-size: 1.3rem;
}

a:hover {
  color: #00d256;
}
</style>
