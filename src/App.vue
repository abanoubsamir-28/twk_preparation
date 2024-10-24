<script>
import useVuelidate from "@vuelidate/core";
import "./assets/styles/stepper-form.css";
import Stepper from "./components/Stepper.vue";
import PersonalInfoVue from "./components/forms/views/PersonalInfo.vue";
import subscriptionModelVue from "./components/forms/views/subscriptionModel.vue";
import AddOnsVue from "./components/forms/views/AddOns.vue";
import SummaryVue from "./components/forms/views/Summary.vue";
import { email, minLength, required } from "@vuelidate/validators";
import Controllers from "./components/Controllers.vue";
import Thankyou from './components/forms/views/Thankyou.vue';

export default {
  setup() {
    return { $v: useVuelidate() };
  },

  components: {
    Stepper,
    Controllers,
    Thankyou
  },
  data() {
    return {
      userCheckedOut : false , 
      formStepperMeta: new Map([
        [
          1,
          {
            index: 1,
            subTitle: "step 1",
            mainTitle: "your info",
            isActive: false,
            formView: PersonalInfoVue,
            formKey: "s1",
            isNext: true,
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
            formKey: "s2",
            isNext: true,
            isBack: true,
            prevFormKey :'s1'
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
            formKey: "s3",
            isNext: true,
            isBack: true,
            prevFormKey :'s2'

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
            formKey: "s4",
            canSubmit: true,
            isBack: true,
            prevFormKey :'s3'

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
          subscriptionModel: false,
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
    toTheNextStep() {
      this.handleStepChange(this.activeStep + 1);
    },
    toTheBackStep() {
      this.handleStepChange(this.activeStep - 1);
    },
    resetFormStepper() {
      this.activeStep = 1;
      this.formStepperMeta.get(1).isActive = true;
    },
    handleStepChange(index) {
      this.formStepperMeta.get(this.activeStep).isActive = false;
      this.formStepperMeta.get(index).isActive = true;
      this.activeStep = index;
    },
    submit() {
      this.userCheckedOut = !this.userCheckedOut
    }
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
        :v="$v"
      ></stepper>
    </div>
    <div v-if="!userCheckedOut">
      <keep-alive>
        <div class="stepper_form--form_view">
          <component
            :v="$v"
            :formModel="stepForm"
            :is="formStepperMeta.get(activeStep).formView"
          ></component>
        </div>
      </keep-alive>
      <controllers
        :v="$v"
        @next-step="toTheNextStep"
        @back-step="toTheBackStep"
        @submit="submit"
        :currentStep="formStepperMeta.get(activeStep)"
      ></controllers>
    </div>
    <thankyou v-else></thankyou>
  </div>
</template>
