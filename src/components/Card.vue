<template>
  <div 
    class="card"
    :class="{'disable' : isDisabled}"
    :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
      width: `${(((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 }px`,
      perspective: `${((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4) * 2 }px`
    }"
    >
    <div 
      class="card__inner" 
      :class="{ 'is-flipped': isFlipped }" 
      
      @click="onToggleFlipped()">
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div class="card__content"
          :style="{
            backgroundImage: `url(${ require('@/assets/' + imageBackFace)})`,
          }">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardFlip",
  props: {
    imageBackFace: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
    },
    rules: {
      type: Array,
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      }
    }
  },
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    }
  },
  methods: {
    onToggleFlipped: function () {
      if(this.rules.length >= 2) return;
      if(this.isDisabled) return;
      this.isFlipped = !this.isFlipped;
      if(this.isFlipped) this.$emit("onFlip", this.card)
    },
    onFlipBackCard: function () {
      this.isFlipped = false;
    },
    onEnableDisableMode: function () {
      this.isDisabled = true;
    },
  }
};
</script>

<style lang="css" scoped="true">
.card {
  display: inline-block;
  margin: 0 1rem 1rem 0;
  width: 90px;
  height: 120px;
}
.card .card__inner {
  width: 100%;
  height: 100%;
  cursor: pointer;
  position: relative;
  transition: transform 1s;
  transform-style: preserve-3d;
}
.card.disable .card__inner {
  cursor: default;
}
.card .card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card .card__inner .card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  padding: 1rem;
  overflow: hidden;
  border-radius: 1rem;
  backface-visibility: hidden;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card .card__inner .card__face.card__face--front .card__content {
  background: url('../assets/images/icon_back.png') no-repeat center center;
  background-size: contain;
  width: 100%;
  height: 100%;
}
.card .card__inner .card__face.card__face--back {
  background: var(--light);
  transform: rotateY(-180deg);
}
.card .card__inner .card__face.card__face--back .card__content {
  width: 100%;
  height: 100%;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center center;
}
</style>
