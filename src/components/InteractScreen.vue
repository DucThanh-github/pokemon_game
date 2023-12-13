<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 64) / Math.sqrt(cardContext.length) - 16) * 3) / 4 + 16) *
          Math.sqrt(cardContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardContext="cardContext"
        @onFlip="checkRules($event)"
      >
      </card-flip>
    </div>
  </div>
</template>
<script>
import CardFlip from "./Card.vue";
export default {
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: { CardFlip },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    async checkRules(card) {
      if (this.rules.length === 2) {
        console.log('thiscards3', this.rules)
        return false};
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("dung");
        this.$refs[`card-${this.rules[0].index}`][0].onEnalbeDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnalbeDisableMode();
        this.rules = [];

        const disabledElement = document.querySelectorAll(
          ".screen .card.disabled"
        );
        console.log(disabledElement);
        if (
          disabledElement.length &&
          disabledElement.length === this.cardContext.length - 2
        ) {
          const timeFinish = new Date().getTime();
          setTimeout(() => {
            this.$emit("onFinish", timeFinish);
            console.log(timeFinish);
          }, 900);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("sai");
        // this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
        // this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
        // this.rules = [];
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        console.log('thiscards1', this.rules)

        }, 800);
        
        // clearTimeout(timeOut);
        
        console.log('thiscards2', this.rules)
      } else return false;
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--dark);
  color: var(--light);
}

.screen__inner {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 2rem auto;
}
</style>