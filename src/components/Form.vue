<template>
  <form>
    <input type="text" name="name" id="name" />
    <input type="email" name="email" id="email" />
    <input type="number" min="1" name="age" id="age" />
    <button type="submit">enviar</button>
  </form>
</template>

<script>
export default {
  name: "FormComp",
};
</script>
