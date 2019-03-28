<template>
  <div class="calculator">
    <div class="display" id="display">{{ current || total || 0 }}</div>
    <div class="button" @click="clear" id="clear">AC</div>
    <div class="button" @click="changeSign">+/-</div>
    <div class="button" @click="percent">%</div>
    <div class="button operator" @click="updateOperator('÷')" id="divide">÷</div>
    <div class="button" @click="updateDisplay('9')" id="nine">9</div>
    <div class="button" @click="updateDisplay('8')" id="eight">8</div>
    <div class="button" @click="updateDisplay('7')" id="seven">7</div>
    <div class="button operator" @click="updateOperator('x')" id="multiply">x</div>
    <div class="button" @click="updateDisplay('6')" id="six">6</div>
    <div class="button" @click="updateDisplay('5')" id="five">5</div>
    <div class="button" @click="updateDisplay('4')" id="four">4</div>
    <div class="button operator" @click="updateOperator('-')" id="subtract">-</div>
    <div class="button" @click="updateDisplay('3')" id="three">3</div>
    <div class="button" @click="updateDisplay('2')" id="two">2</div>
    <div class="button" @click="updateDisplay('1')" id="one">1</div>
    <div class="button operator" @click="updateOperator('+')" id="add">+</div>
    <div class="button zero" @click="updateDisplay('0')" id="zero">0</div>
    <div class="button" @click="decimal" id="decimal">.</div>
    <div class="button operator" @click="calculate" id="equals">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      previous: "",
      current: "",
      total: "",
      operator: ""
    };
  },
  methods: {
    updateDisplay(num) {
      if (num === "0" && !this.current.length) {
        return;
      }
      this.current += num;
    },
    decimal() {
      if (this.current.includes(".")) {
        return;
      }
      if (!this.current.length) {
        this.current = "0.";
        return;
      }
      this.current += ".";
    },
    clear() {
      this.current = "";
      this.previous = "";
      this.operator = "";
      this.total = "";
    },
    changeSign() {
      if (!this.current.length) {
        return;
      }
      if (this.current.match("-")) {
        this.current = this.current.slice(1);
        return;
      }
      this.current = "-".concat(this.current);
    },
    percent() {
      this.current = (parseFloat(this.current) / 100).toString();
    },
    updateOperator(operator) {
      if (!this.current && !this.total) {
        return;
      }
      if ((this.operator && this.previous) || (this.operator && this.total)) {
        this.calculate();
      }
      this.previous = this.current;
      this.current = "";
      this.operator = operator;
    },
    calculate() {
      if (this.total) {
        this.previous = this.total;
      }
      switch (this.operator) {
        case "+":
          this.total = parseFloat(this.previous) + parseFloat(this.current);
          break;
        case "-":
          this.total = parseFloat(this.previous) - parseFloat(this.current);
          break;
        case "x":
          this.total = parseFloat(this.previous) * parseFloat(this.current);
          break;
        default:
          this.total = parseFloat(this.previous) / parseFloat(this.current);
          break;
      }
      this.previous = "";
      this.current = "";
      this.operator = "";
    }
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
  max-width: 100%;
  overflow: hidden;
  grid-area: display;
  padding-right: 1rem;
  padding-bottom: 1rem;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  font-size: 4rem;
  background-color: #35495e;
  border: 1px solid #aaaaaa;
}
.button {
  border: 1px solid #aaaaaa;
  background-color: #fafafa;
  color: #35495e;
  display: flex;
  justify-content: center;
  align-items: center;
}
.button:active {
  transform: scale(0.99);
  box-shadow: 0px 0px 3px #35495e;
}
.button:hover {
  cursor: pointer;
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
