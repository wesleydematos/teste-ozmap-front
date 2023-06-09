<template>
  <HeaderComp />
  <Users />
  <Register />
</template>

<script>
import HeaderComp from "./components/Header.vue";
import Users from "./pages/Users.vue";
import Register from "./pages/Register.vue";

export default {
  name: "App",
  components: {
    HeaderComp,
    Users,
    Register,
  },
};
</script>

<style>
body {
  background-color: #1d1d1d;
  color: #ffffff;
  padding: 0;
  margin: 0;
}

button,
a {
  cursor: pointer;
}

ul,
ol,
li {
  list-style: none;
}
</style>
