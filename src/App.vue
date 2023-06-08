<template>
  <HeaderComp />
  <FormComp />
</template>

<script>
import HeaderComp from "./components/Header.vue";
import FormComp from "./components/Form.vue";

export default {
  name: "App",
  components: {
    HeaderComp,
    FormComp,
  },
};
</script>
