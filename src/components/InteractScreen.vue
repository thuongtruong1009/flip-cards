<template>
  <div>
    <h2>Playing game</h2>
    <Cardo
      class="screen"
      v-for="(card, index) in cardContext"
      :cardContext="cardContext"
      :ref="`card-${index}`"
      :key="index"
      :imgBackFaceUrl="`/images/${card}.png'`"
      :card="{ index, value: card }"
      @onFlip="checkRule($event)"
    />
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: { Cardo: Card },
  data() {
    return {
      rules: []
    }
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      console.log(this.rules);

      if ((this.rules.length === 2) && (this.rules[0].value === this.rules[1].value)) {
        console.log("done");
        //add class disabled to card and reset length of rules
        this.$refs[`card-${this.rules[0].index}`].onDisabledMode();
        this.$refs[`card-${this.rules[1].index}`].onDisabledMode();
        this.rules = [];

        const disabledElements = document.querySelectorAll(".screen .card.disabled");
        console.log(disabledElements);

        if (disabledElements && (disabledElements.length === this.cardContext.length-2)) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 900)
        }

      } else if ((this.rules.length === 2) && (this.rules[0].value !== this.rules[1].value)) {
        console.log('yet');
        //close two card and reset length of rules
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`].onFlipBackCard();
          this.rules = [];
        }, 800)
      } else return false;
    }
  }
};
</script>