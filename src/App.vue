<script>
import "./assets/styles/stepper-form.css";
import Stepper from "./components/Stepper.vue";
export default {
  components: {
    Stepper,
  },
  data() {
    return {
      formStepperMeta: new Map([
        [
          1,
          {
            index: 1,
            subTitle: "step 1",
            mainTitle: "your info",
            isActive: false,
          },
        ],
        [
          2,
          {
            index: 2,
            subTitle: "step 2",
            mainTitle: "select plan",
            isActive: false,
          },
        ],
        [
          3,
          {
            index: 3,
            subTitle: "step 3",
            mainTitle: "add-ons",
            isActive: false,
          },
        ],
        [
          4,
          {
            index: 4,
            subTitle: "step 4",
            mainTitle: "summary",
            isActive: false,
          },
        ],
      ]),
      activeStep: null,
    };
  },
  computed: {
    stepperEntries() {
      return Array.from(this.formStepperMeta.values());
    },
  },
  methods: {
    resetFormStepper() {
      this.activeStep = 1;
      this.formStepperMeta.get(1).isActive = true;
    },
    handleStepChange(index) {
      this.formStepperMeta.get(this.activeStep).isActive = false;
      this.formStepperMeta.get(index).isActive = true;
      this.activeStep = index;
    },
  },
  mounted() {
    this.resetFormStepper();
  },
};
</script>

<template>
  <div class="stepper_form">
    <div class="step_form__navigation">
      <stepper
        @step-clicked="handleStepChange"
        v-for="item in stepperEntries"
        :step="item"
        :key="item.index"
      ></stepper>
    </div>
  </div>
</template>
