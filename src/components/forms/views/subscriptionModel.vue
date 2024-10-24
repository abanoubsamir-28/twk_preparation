<script>
import FormHeader from "../FormHeader.vue";
import BaseInput from "../UI/BaseInput.vue";
import arcadeIcon from "../../../assets/images/icon-arcade.svg";
import advancedIcon from "../../../assets/images/icon-advanced.svg";
import proIcon from "../../../assets/images/icon-pro.svg";

export default {
  components: { FormHeader, BaseInput },
  props: ["v", "formModel"],
  data() {
    return {
      cardsConfig: new Map([
        [
          "arcade",
          {
            title: "arcade",
            iconPath: arcadeIcon,
            monthlyFees: 9,
            isActive: false,
            yearlyFees: 90,
          },
        ],
        [
          "advanced",
          {
            title: "advanced",
            iconPath: advancedIcon,
            monthlyFees: 12,
            isActive: false,
            yearlyFees: 120,
          },
        ],
        [
          "pro",
          {
            title: "pro",
            iconPath: proIcon,
            monthlyFees: 15,
            isActive: false,
            yearlyFees: 150,
          },
        ],
      ]),
      activeCard: null,
      switchValue: false,
    };
  },
  computed: {
    cards() {
      return Array.from(this.cardsConfig.values());
    },
    currentPlanType () {
      return this.formModel.s2.subscriptionModel
    }
  },
  methods: {
    handleCardChange(cardKey) {
      this.cardsConfig.get(this.activeCard).isActive = false;
      this.activeCard = cardKey.title;
      this.cardsConfig.get(cardKey.title).isActive = true;
      this.formModel.s2.plan = cardKey;
    },
  },
  mounted() {
    console.log(this.formModel);
    if(!this.formModel.s2.plan) {
      this.activeCard = "pro";
      this.cardsConfig.get("pro").isActive = true;
    } else {
      console.log("Done");
      this.activeCard = this.formModel.s2.plan.title;
      this.cardsConfig.get(this.formModel.s2.plan.title).isActive = true;
    }
  },
};
</script>

<template>
  <form-header
    title="select your plan"
    subTitle="you have the options of monthly or yearly billing"
  ></form-header>
  <div class="cards">
    <div
      @click="handleCardChange(card)"
      v-for="card of cards"
      :key="card.title"
      class="card"
      :class="{ active: card.isActive }"
    >
      <img :src="card.iconPath" alt="" width="30" height="30"/>
      <div class="card_content">
        <h5>{{ card.title }}</h5>
        <p v-if="currentPlanType" class="card-fees">${{ card.yearlyFees }}/yr</p>
        <p v-else class="card-fees">${{ card.monthlyFees }}/m</p>
        <p v-if="currentPlanType" class="card-offer">2 months free</p>
      </div>
    </div>
  </div>
  <div class="fees_type">
    <div class="fees_type--container">
      <p>Monthly</p>
      <b-form-checkbox
        v-model="formModel.s2.subscriptionModel"
        name="check-button"
        switch
      >
      </b-form-checkbox>
      <p>yearly</p>
    </div>
  </div>
</template>

<style scoped>
h1 {
  color: red;
}
.cards {
  display: flex;
  gap: 1rem;
}
.card {
  padding: 1.5rem 0.8rem;
  border: 1px solid #e3e8ef;
  border-radius: 12px;
  cursor: pointer;
  width: 120px;

}
img {
  margin-bottom: 1.6rem;
}
h5 {
  font-family: "Ubuntu", sans-serif;
  margin-bottom: 0.5rem;
  font-weight: 700;
  text-transform: capitalize;
  color: #1a2e4d;
}
.card-fees {
  color: #a1b2c2;
  font-weight: 400;
  font-size: 0.9rem;
}
.card-offer {
  color: #1a2e4d;
  font-size: 0.8rem;
  text-wrap: nowrap;
  margin-top: 1rem;
  font-weight: 500;
}
.active {
  border: 1px solid #7f3f8c;
  background: #f4fbfe;
}
.fees_type {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 1rem;
  text-transform: capitalize;
  font-weight: bold;
  background: #f4fbfe;
  padding: 5px 0;
}
.fees_type--container {
  display: flex;
  gap: 10px;
  align-items: center;
}
@media (max-width: 1280px) {
  .cards{
    flex-direction: column;
  }
  .card {
    display: flex;
    width: 99%;
    flex-direction: row;
    gap: 1rem;
    height: fit-content;
    padding: .4rem 0.5rem;
    margin: auto;
    align-items: center;
  }
  .card img {
    margin: unset;
  }
}

</style>
