<script>
import "../assets/styles/stepper-form.css";
export default {
  props: ["step", "v"],
  methods: {
    handleStepClick() {
      if (this.isThisStepAvailable) {
        this.$emit("step-clicked", this.step.index);
      }
    },
  },
  computed: {
    isThisStepAvailable() {
      return !this.v.stepForm[this.step.prevFormKey].$invalid;
    },
  },
};
</script>

<template>
  <div
    class="form_stepper"
    :class="{ active: step.isActive }"
    @click="handleStepClick"
  >
    <p class="form_stepper__step">{{ step.index }}</p>
    <div class="form_stepper__info">
      <p class="ubuntu-regular">{{ step.subTitle }}</p>
      <p class="ubuntu-medium">{{ step.mainTitle }}</p>
    </div>
  </div>
</template>
