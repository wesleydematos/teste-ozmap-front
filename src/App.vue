<template>
  <div class="app-container">
    <HeaderComp />
    <div>
      <router-view />
    </div>
  </div>
  <div class="footer">
    <FooterComp />
  </div>
</template>

<script>
import HeaderComp from "./components/Header.vue";
import FooterComp from "./components/Footer";

export default {
  name: "App",
  components: {
    HeaderComp,
    FooterComp,
  },
};
</script>

<style>
* {
  font-family: Helvetica;
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
  box-sizing: border-box;
}

body {
  color: #ffffff;
  background-color: #1d1d1d;
}

button,
a {
  cursor: pointer;
  text-decoration: none;
}

a {
  color: #ffffff;
}

.app-container {
  min-height: calc(100vh - 5rem);
  display: flex;
  flex-direction: column;
}

.footer {
  margin-top: auto;
}
</style>
