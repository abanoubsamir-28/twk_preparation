<script>
import "../assets/styles/stepper-form.css";
export default {
  props: {
    step: Object,
  },
  methods :{
    handleStepClick () {
        this.$emit('step-clicked' , this.step.index)
    }
  }
};
</script>

<template>
  <div class="form_stepper " :class="{ active: step.isActive }" @click="handleStepClick">
    <p class="form_stepper__step ">{{ step.index }}</p>
    <div class="form_stepper__info">
      <p class="ubuntu-regular">{{ step.subTitle }}</p>
      <p class="ubuntu-medium">{{ step.mainTitle }}</p>
    </div>
  </div>
</template>
