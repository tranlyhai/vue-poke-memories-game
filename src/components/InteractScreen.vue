<template>
  <section class="interact__screen">
    <div 
      class="screen__inner"
      :style="{
        width: `${((((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4)) + 16) * Math.sqrt(cardsContext.length)  }px`
      }"
    >
      <card-flip 
        v-for="(card, index) in cardsContext" 
        :key="index"
        :ref="`card-${index}`"
        :image-back-face="`images/${card}.png`"
        :card="{index, value: card}"
        :rules="rules"
        :cardsContext="cardsContext"
        @onFlip="checkRules($event)"
        />
    </div>
  </section>
</template>

<script>
import CardFlip from './Card.vue';
export default {
  name: 'InteractScreen',
  props: {
    cardsContext: {
      type: Array,
      validator: function(value) {
        return Array.isArray(value) ? value : [];
      }
    }
  },
  components: {
    CardFlip
  },
  data() {
    return {
      rules: []
    }
  },
  methods: {
    checkRules: function(card) {
      if(this.rules.length === 2) return false;
      this.rules.push(card);
      if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value) {
        console.log("Right...");
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableMode();
        // reset
        this.rules = [];
        const disableElements = document.querySelectorAll(".interact__screen .card.disable");
        
        if(disableElements && disableElements.length === (this.cardsContext.length - 2)) {
          setTimeout(() => {
            this.$emit("onFinshed");
          }, 950);
        }
      } else if(this.rules.length === 2 && this.rules[0].value !== this.rules[1].value) {
        console.log("Wrong...");
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          // reset the rules
          this.rules = [];
        }, 800);
      } else return false;
    }
  }
}
</script>

<style lang="css" scoped>
.interact__screen {
  top: 0;
  left: 0;
  z-index: 2;
  width: 100%;
  min-height: 100vh;
  position: absolute;
  background: var(--dark);
  color: var(--light);
}
.interact__screen .screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
