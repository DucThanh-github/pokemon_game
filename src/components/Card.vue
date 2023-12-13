<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height: `${(920 - 64) / Math.sqrt(cardContext.length) - 16}px`,
      width: `${(((920 - 64) / Math.sqrt(cardContext.length) - 16) * 3) / 4}px`,
      perspective: `${(((920 - 64) / Math.sqrt(cardContext.length) - 16) * 3) / 2}px`
    }"
  >
    <div
      class="card__inner"
      @click="onToggleFlipCard"
      :class="{ 'is-flipped': isFliped }"
    >
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{
            backgroundSize: `${
              (((920 - 64) / Math.sqrt(cardContext.length) - 16) * 3) / 12
            }px ${
              (((920 - 64) / Math.sqrt(cardContext.length) - 16) * 3) / 12
            }px`,
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Array, Number, Object],
    },
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isDisabled: false,
      isFliped: false,
    };
  },

  methods: {
    onToggleFlipCard() {
      if (this.isDisabled) return false;
      this.isFliped = !this.isFliped;
      if (this.isFliped) {
        this.$emit("onFlip", this.card);
      } else return false;
    },
    onFlipBackCard() {
      this.isFliped = false;
    },
    onEnalbeDisableMode() {
      this.isDisabled = true;
    },
  },
};
</script>


<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.card.disabled .card__inner {
  cursor: default;
}
.card__inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 0.5rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.3);
}

.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  height: 100%;
  width: 100%;
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card__face--back .card__content {
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
</style>
