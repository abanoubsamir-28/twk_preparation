<script>
import FormHeader from "../FormHeader.vue";
import BaseInput from "../UI/BaseInput.vue";
export default {
  components: { FormHeader, BaseInput },
  props: ["model"],
};
</script>

<template>
  <form-header
    title="personal info"
    subTitle="please provide your name, email address, and phone number"
  ></form-header>
  
  <base-input
    :model="model.s1.name"
    placeholder="First Name"
    type="text"
    label="Name"
  ></base-input>
  <!-- <button @click="console.log(model)">Click</button> -->
</template>


