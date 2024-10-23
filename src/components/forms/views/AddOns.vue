<script>
import FormHeader from "../FormHeader.vue";

export default {
  components: { FormHeader },
  props: ["v", "formModel"],
  data() {
    return {
      addOnsMap: new Map([
        [
          1,
          {
            id: 1,
            title: "online service",
            slug: "access to multiplayer games",
            feesM: 1,
            feesY: 10,
          },
        ],
        [
          2,
          {
            id: 2,
            title: "large storage",
            slug: "extra 1TB cloud save",
            feesM: 2,
            feesY: 20,
          },
        ],
        [
          3,
          {
            id: 3,
            title: "customizable profile",
            slug: "custom theme on your profile",
            feesM: 2,
            feesY: 20,
          },
        ],
      ]),
    };
  },
  computed: {
    addons() {
      return Array.from(this.addOnsMap.values());
    },
    currentFeesType() {
      return this.formModel.s2.subscriptionModel;
    },
  },
  methods: {
    isChecked(id) {
      return this.formModel.s3.addOns.some((item) => item.id === id);
    },
    handleToggle(addon) {
      const addonExists = this.isChecked(addon.id);

      if (addonExists) {
        this.formModel.s3.addOns = this.formModel.s3.addOns.filter(
          (item) => item.id !== addon.id
        );
      } else {
        this.formModel.s3.addOns.push(addon);
      }
    },
  },
};
</script>

<template>
  <form-header
    title="Pick add-ons"
    subTitle="add-ons help enhance your gaming experience"
  ></form-header>
  <div
    v-for="addon in addons"
    :key="addon.id"
    @click="handleToggle(addon)"
    class="add_ons--checker"
    :class="{ active: isChecked(addon.id) }"
  >
    <div class="main_content">
      <input type="checkbox" :checked="isChecked(addon.id)" />
      <div class="add_ons--checker_content">
        <h6>{{ addon.title }}</h6>
        <p>{{ addon.slug }}</p>
      </div>
    </div>
    <div v-if="currentFeesType" class="add_ons--checker_fees">
      +${{ addon.feesY }}/y
    </div>
    <div v-else class="add_ons--checker_fees">+${{ addon.feesM }}/m</div>
  </div>
</template>

<style scoped>
.add_ons--checker {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 2rem;
  border: 1px solid #7f3f8c;
  padding: 1rem;
  border-radius: 12px;
  text-transform: capitalize;
  cursor: pointer;
  margin: 1rem 0;
}
.main_content {
  display: flex;
  gap: 1rem;
  text-wrap: nowrap;
}
.add_ons--checker_content h6 {
  font-weight: bold;
  color: #1a2e4d;
  margin-bottom: 5px;
}
.add_ons--checker_content p {
  color: #a1b2c2;
}
.add_ons--checker_fees {
  color: #1a2e4d;
  font-weight: bold;
}
</style>
