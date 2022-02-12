<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div class="operator" @click="clear">C</div>
    <div class="operator" @click="plus">+</div>
    <div class="operator" @click="minus">-</div>
    <div class="operator" @click="percent">%</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="operator" @click="division">/</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="operator" @click="multiplication">*</div>

    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="equal" @click="equal">=</div>

    <div class="btn" @click="append('0')">0</div>
    <div @click="dot" class="btn">.</div>
    <div class="operator" @click="root">√</div>
    <div class="change" @click="advance">Sc</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pervious: null,
      current: "",
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(num) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`;
    },
    setPrevious() {
      this.pervious = this.current;
      this.operatorClicked = true;
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.pervious)
      )}`;
      this.pervious = null;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    multiplication() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    division() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    root() {
      this.operator = (a) => Math.sqrt(a);
      this.setPrevious();
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.display {
  grid-column: 1 / 5;
  background-color: rgb(209, 28, 28);
  color: white;
}
.btn {
  background-color: aqua;
  border: 1px solid #999;
}
.calculator {
  margin: auto;
  width: 400px;
  font-size: 50px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.operator {
  background-color: orange;
  border: 1px solid #999;
}
.equal {
  background-color: orange;
}
</style>
