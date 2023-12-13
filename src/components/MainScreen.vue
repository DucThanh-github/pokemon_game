<template>
  <div class="main">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>

<style lang="css" scoped>
.main {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: var(--dark);
  color: var(--light);
}
.main h1 {
  font-size: 72px;
}
.main h3 {
  font-size: 32px;
  padding: 1rem 0 2rem;
}
.actions {
  display: flex;
}
.actions button {
  font-family: "Odibee Sans", cursive;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 150px;
  height: 150px;
  font-size: 2rem;
  margin: 0 1rem;
  color: var(--light);
  background-color: var(--dark);
  border: solid 1px var(--light);
  border-radius: 1rem;
}
.actions button:hover {
  cursor: pointer;
  background-color: var(--light);
  color: var(--dark);
  transition-duration: 0.3s;
  transition-timing-function: ease-in-out;
  transition-delay: 0s;
}
</style>
