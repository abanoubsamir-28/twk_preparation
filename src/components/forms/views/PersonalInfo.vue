<script>
import FormHeader from "../FormHeader.vue";
import BaseInput from "../UI/BaseInput.vue";
export default {
  components: { FormHeader, BaseInput },
  props: ["v", "formModel"],
};
</script>

<template>
  <form-header
    title="personal info"
    subTitle="please provide your name, email address, and phone number"
  ></form-header>

  <base-input
    v-model="formModel.s1.name"
    :v="v.stepForm.s1.name"
    placeholder="First Name"
    type="text"
    label="Name"
  ></base-input>
  <base-input
    v-model="formModel.s1.email"
    :v="v.stepForm.s1.email"
    placeholder="blablabla@gmail.com"
    type="email"
    label="Email"
  ></base-input>
  <base-input
    v-model="formModel.s1.phone"
    :v="v.stepForm.s1.phone"
    placeholder="e.g +20 100 543 4984"
    type="tel"
    label="Phone Number"
  ></base-input>
</template>
