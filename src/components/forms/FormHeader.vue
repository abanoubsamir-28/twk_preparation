<script>
export default {
  props: ["title", "subTitle"],
};
</script>

<template>
  <header class="form-header">
    <h2 class="ubuntu-bold">{{ title }}</h2>
    <p class="ubuntu-medium">{{ subTitle }}</p>
  </header>
  
</template>

<style scoped>
h2,
p {
  text-transform: capitalize  ;
}
</style>
