<script>
import useVuelidate from "@vuelidate/core";
import "./assets/styles/stepper-form.css";
import Stepper from "./components/Stepper.vue";
import PersonalInfoVue from "./components/forms/views/PersonalInfo.vue";
import subscriptionModelVue from "./components/forms/views/subscriptionModel.vue";
import AddOnsVue from "./components/forms/views/AddOns.vue";
import SummaryVue from "./components/forms/views/Summary.vue";
import { email, minLength, required } from "@vuelidate/validators";
export default {
  setup() {
    return { $v: useVuelidate() };
  },

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
            formView: PersonalInfoVue,
          },
        ],
        [
          2,
          {
            index: 2,
            subTitle: "step 2",
            mainTitle: "select plan",
            isActive: false,
            formView: subscriptionModelVue,
          },
        ],
        [
          3,
          {
            index: 3,
            subTitle: "step 3",
            mainTitle: "add-ons",
            isActive: false,
            formView: AddOnsVue,
          },
        ],
        [
          4,
          {
            index: 4,
            subTitle: "step 4",
            mainTitle: "summary",
            isActive: false,
            formView: SummaryVue,
          },
        ],
      ]),
      activeStep: null,
      stepForm: {
        s1: {
          name: "",
          email: "",
          phone: "",
        },
        s2: {
          plan: null,
          subscriptionModel: 1,
        },
        s3: {
          addOns: [],
        },
      },
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
  validations() {
    return {
      stepForm: {
        s1: {
          name: { required },
          email: { required, email },
          phone: { required, minLength: minLength(10) },
        },
        s2: {
          plan: { required },
          subscriptionModel: { required },
        },
        s3: {
          addOns: { required },
        },
      },
    };
  },
  beforeMount() {
    this.resetFormStepper();
  },
  mounted () {
    console.log(this.$v);
  }
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
    <keep-alive>
      <div class="stepper_form--form_view">
        <component
          :model="$v.stepForm"
          :is="formStepperMeta.get(activeStep).formView"
        ></component>
      </div>
    </keep-alive>
    <!-- <h1>{{$v.stepForm.s1.name.value}}</h1> -->
  </div>
</template>
