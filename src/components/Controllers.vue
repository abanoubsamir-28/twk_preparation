<script>
export default {
  props: ["currentStep", "v"],
  computed: {
    currentStepValidation() {
      return this.v.stepForm[this.currentStep.formKey];
    },
    canContinueToTheNext() {
      if (!this.currentStepValidation) {
        return true;
      }
      return !this.currentStepValidation.$invalid;
    },
  },
  methods: {
    goToNextStep() {
      this.$emit("next-step");
    },
    goToBackStep() {
      this.$emit("back-step");
    },
    submit() {
      this.$emit("submit");
    },
  },
};
</script>

<template>
  <div class="controllers">
    <button
      @click="goToBackStep"
      :style="{ visibility: currentStep.isBack ? 'visible' : 'hidden' }"
      class="back-btn"
    >
      go back
    </button>
    <button
      v-if="!currentStep.canSubmit"
      @click="goToNextStep"
      class="next-btn"
      :class="{ disabled: !canContinueToTheNext }"
    >
      next
    </button>
    <button
      v-else
      @click="submit"
      class="next-btn"
      :class="{ disabled: !canContinueToTheNext }"
    >
      submit
    </button>
  </div>
</template>

<style>
.controllers {
  margin: auto;
  display: flex;
  justify-content: space-between;
  width: 80%;
}
.next-btn {
  padding: 0.5rem 1.7rem;
  border-radius: 6px;
  border: none;
  background: #174a8b;
  color: white;
  text-transform: capitalize;
}
.disabled {
  background: #17498b67;
  pointer-events: none;
}
.back-btn {
  color: #a1b2c2;
  border: none;
  background: transparent;
  text-transform: capitalize;
}
.back-btn:hover {
  color: #174a8b;
}

@media (max-width: 1280px) {
  .controllers {
    position: absolute;
    bottom: 1rem;
    background: white;
    width: 100%;
    padding: 1rem 2rem;
    left: 0;
  }
}
</style>
