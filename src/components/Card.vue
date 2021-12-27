<template>
  <div class="card" v-bind:class="{disabled : isDisabled}">
    <div
      class="card-inner"
      :class="{ 'is-Focus': isFliped }"
      @click="onToggleFliped"
    >
      <div class="card-front">
        <div class="card-front-content"></div>
      </div>
      <div class="card-back">
        <div
          class="card-back-content"
          :style="{
            //backgroundImage: `url(${require('~/assets/' + imgBackFaceUrl)})`,
            //backgroundImage: `url('~/assets/' + imgBackFaceUrl)`,
            backgroundImage: `url('/src/assets/${imgBackFaceUrl})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    card:{
      type: [String, Array, Object, Number]
    },
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isFliped: false,
      isDisabled: false
    };
  },
  methods: {
    onToggleFliped() {
      if(this.isDisabled) return false;
      this.isFliped = !this.isFliped;
      if(this.isFliped) this.$emit("onFlip", this.card);
    },
    onFlipBackCard(){
      this.isFliped = false;
    },
    onDisabledMode(){
      this.isDisabled = true;
    }
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  width: 90px;
  height: 120px;
  perspective: 500px;
  color: black;
  margin: 10px;
  transition: 0.5s linear;
}
.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  text-align: center;
  transition: 0.8s;
  cursor: pointer;
}
.card.disabled .card-inner{
  cursor:not-allowed;
}
.card-inner.is-Focus {
  transform: rotateY(180deg) translateX(-10px);
}
.card-front,
.card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  overflow: hidden;
  padding: 5px;
  border-radius: 15px;
}
.card-front {
  background: var(--light);
}
.card-back {
  background: var(--light);
  transform: rotateY(-180deg);
}
.card-front-content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 40px 40px;
  height: 100%;
  width: 100%;
}
.card-back-content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
  z-index: 999;
}
</style>