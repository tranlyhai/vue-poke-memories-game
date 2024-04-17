<template>
  <section class="main__screen">
    <h1>poke games</h1>
    <p>Select mode to start game</p>
    <div class="modes">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>easy</span>
      </button>
      <button @click="onStart(32)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>super hard</span>
      </button>
    </div>
  </section>
</template>

<script>
export default {
  name: "MainScreen",
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", {totalOfBlocks});
    }
  }
};
</script>

<style lang="css" scoped>
.main__screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: var(--dark);
  color: var(--light);
}

.main__screen h1 {
  font-size: 4.5rem;
  letter-spacing: 4px;
  text-transform: uppercase;
}

.main__screen p {
  font-size: 2rem;
  letter-spacing: 1px;
}

.modes {
  display: flex;
  margin-top: 2rem;
}

.modes button {
  font: var(--font);
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

.modes button:hover {
  background-color: var(--light);
  color: var(--dark);
}

.modes button span:first-child {
  font-size: 2rem;
  letter-spacing: 5px;
}

.modes button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
  text-transform: capitalize;
  letter-spacing: 1.5px;
}
</style>
