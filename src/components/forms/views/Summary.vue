<script>
import FormHeader from "../FormHeader.vue";

export default {
  components: { FormHeader },
  props: ["v", "formModel"],
  computed: {
    summaryData() {
      const { subscriptionModel: isYearlyPlan, plan } = this.formModel.s2;
      const planPrice = isYearlyPlan ? plan.yearlyFees : plan.monthlyFees;

      const addOnsSummary = this.formModel.s3.addOns.map(({ title, feesY, feesM }) => ({
        title,
        price: isYearlyPlan ? feesY : feesM,
      }));

      const addOnsTotalPrice = addOnsSummary.reduce((total, { price }) => total + price, 0);

      return {
        planPrice,
        addOnsSummary,
        totalPrice: planPrice + addOnsTotalPrice,
        plan,
        isYearlyPlan,
      };
    },
  },
};
</script>

<template>
  <form-header
    title="Finishing up"
    subTitle="Double check everything looks ok before confirming"
  ></form-header>

  <div class="summary">
    <div class="summary-content">
      <div class="plan">
        <div class="content">
          <h5>
            {{ summaryData.plan.title }} ({{ summaryData.isYearlyPlan ? "yearly" : "monthly" }})
          </h5>
          <p>change</p>
        </div>
        <div class="price">
          ${{ summaryData.planPrice }}/{{ summaryData.isYearlyPlan ? "yr" : "mo" }}
        </div>
      </div>

      <div class="line"></div>

      <div class="addOns">
        <div
          v-for="addon in summaryData.addOnsSummary"
          :key="addon.title"
          class="addon"
        >
          <p>{{ addon.title }}</p>
          <p>+${{ addon.price }}/{{ summaryData.isYearlyPlan ? "yr" : "mo" }}</p>
        </div>
      </div>
    </div>

    <div class="total">
      <p>Total ({{ summaryData.isYearlyPlan ? "per year" : "per month" }})</p>
      <p class="total-price">${{ summaryData.totalPrice }} / {{ summaryData.isYearlyPlan ? "yr" : "mo" }}</p>
    </div>
  </div>
</template>

<style scoped>
.summary {
  padding: 1rem;
}
.summary-content {
  background: #f4fbfe;
  border-radius: 12px;
  padding: 1rem .5rem;
}
.plan {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.plan h5,
.price {
  font-weight: bold;
  color: #1a2e4d;
  margin-bottom: 5px;
}
.plan p {
  color: #a1b2c2;
  font-size: 14px;
  text-decoration: underline;
  cursor: pointer;
  transition: color 0.5s;
}
.plan p:hover {
  color: #1a2e4d;
}
.content {
  text-transform: capitalize;
}
.line {
  margin: 1rem auto;
  width: 95%;
  height: 1px;
  background: #a1b2c2;
}
.addon {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #a1b2c2;
  text-transform: capitalize;
  margin: 0.6rem 0;
}
.addon p:nth-child(2) {
  color: #1a2e4d;
}
.total {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #a1b2c2;
  margin: 1rem 0;
}
.total-price {
  font-size: 1.4rem;
  color: #1a2e4d;
  font-weight: bold;
}
</style>
