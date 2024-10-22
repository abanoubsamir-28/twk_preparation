<script>
export default {
  props: ["model", "placeholder", "type", "label", "name"],
  methods: {
    handleInput(e) {
      this.model.value = e.target.value;
    },
  },
};
</script>

<template>
  <label :for="name">{{ label }}</label>
  <input
    :name="name"
    :value="model.value"
    :placeholder="placeholder"
    :type="type"
    @input="handleInput"
  />
</template>

<style scoped>
label {
  display: block;
  margin-bottom: 5px;
  color: #1a2e4d;
}
input {
  border: 1px solid #e3e8ef;
  padding: 0.7rem 0.4rem;
  width: 100%;
  border-radius: 5px;
  outline: none;
}
input:focus {
  border: 1px solid #7f3f8c;
}
input::placeholder {
  color: #e3e8ef;
}
</style>
