<script>
export default {
  props: ["modelValue", "placeholder", "type", "label", "name", "v"],
  methods: {
    handleInput(e) {
      this.$emit("update:modelValue", e.target.value);
    },
  },
};
</script>

<template>
  <div>
    <header>
      <label :for="name">{{ label }}</label>
      <div :class="{ error: v.$errors.length }">
        <div class="input-errors" v-for="error of v.$errors" :key="error.$uid">
          <div class="error-msg">{{ error.$message }}</div>
        </div>
      </div>
    </header>
    <input
      :name="name"
      :value="modelValue"
      :placeholder="placeholder"
      :type="type"
      @input="handleInput"
      @blur="v.$touch()"
    />
  </div>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
  align-items: baseline;
}
label {
  display: block;
  margin-bottom: 5px;
  color: #1a2e4d;
  font-weight: 500;
  font-size: 0.8rem;
}
input {
  border: 1px solid #e3e8ef;
  padding: 0.7rem 0.4rem;
  width: 100%;
  border-radius: 5px;
  outline: none;
  margin-bottom: 1.5rem;
}
input:focus {
  border: 1px solid #7f3f8c;
}
input::placeholder {
  color: #a1b2c2;
  font-family: "ubuntu-bold";
  font-weight: 500;
}
.error {
  color: #e54a3d;
  font-weight: 700;
}
</style>
