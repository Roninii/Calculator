<template>
  <div class="calculator">
    <div class="display">{{ current }}</div>
    <div class="button">AC</div>
    <div class="button">+/-</div>
    <div class="button">%</div>
    <div class="button operator">÷</div>
    <div class="button">9</div>
    <div class="button">8</div>
    <div class="button">7</div>
    <div class="button operator">x</div>
    <div class="button">6</div>
    <div class="button">5</div>
    <div class="button">4</div>
    <div class="button operator">-</div>
    <div class="button">3</div>
    <div class="button">2</div>
    <div class="button">1</div>
    <div class="button operator">+</div>
    <div class="button zero">0</div>
    <div class="button">.</div>
    <div class="button operator">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      current: ``
    };
  }
};
</script>

<style scoped>
.calculator {
  display: grid;
  margin: 0 auto;
  height: 100%;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(6, 1fr);
  grid-template-areas:
    "display display display display"
    "clear sign percent divide"
    "seven eight nine multiply"
    "four five six subtract"
    "one two three add"
    "zero zero decimal equal";
  color: #fafafa;
  font-size: 1.5rem;
}
.display {
  grid-area: display;
  padding-right: 1rem;
  padding-bottom: 1rem;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  font-size: 3rem;
  background-color: #3a3a3a;
  border: 1px solid #aaaaaa;
}
.button {
  border: 1px solid #aaaaaa;
  background-color: #fafafa;
  color: #3a3a3a;
  display: flex;
  justify-content: center;
  align-items: center;
}
.zero {
  grid-area: zero;
}
.operator {
  border: 1px solid #aaaaaa;
  background-color: #41b883;
  color: #fafafa;
}
</style>
