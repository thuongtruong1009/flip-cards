<template>
  <h2>Play flip 3D card game</h2>
  <div class="actions">
    <button @click="onStart(16)">
      <span>4x4</span>
      <span>Easy</span>
    </button>
    <button @click="onStart(36)">
      <span>6x6</span>
      <span>Medium</span>
    </button>
    <button @click="onStart(64)">
      <span>8x8</span>
      <span>Hard</span>
    </button>
    <button @click="onStart(100)">
      <span>10x10</span>
      <span>Pro</span>
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalBlocks) {
      this.$emit("onStart", { totalBlocks });
    },
  },
};
</script>

<style scoped>
.actions {
  display: flex;
  justify-content: center;
  align-items: center;
  grid-gap: 30px;
}
.actions > button {
  border-radius: 20px;
  outline: none;
  border: none;
  display: grid;
  justify-content: center;
  align-items: center;
  width: 120px;
  height: 120px;
  font-size: 1.2em;
  box-shadow: 1px 1px 2px rgb(255, 255, 255);
  transition: 0.4s;
  cursor: pointer;
  background: rgba(255, 255, 255, 0.767);
}

.actions > button > span {
  background: transparent;
}
.actions > button:hover {
  transform: scale(1.1) translateY(-10px);
  box-shadow: 3px 3px 7px gray;
  background: transparent;
  color: white;
  border: 1px solid gray;
}
</style>
