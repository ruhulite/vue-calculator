<template>
  <div class="calculator">
    <h2>Vue.js <br />A simple Functional Calculator</h2>
    <div class="calculator-wrap">
      <div class="display">{{ current || '0' }}</div>
      <div @click="clear" class="btn clear">C</div>
      <div @click="sign" class="btn ">+/-</div>
      <div @click="percent" class="btn ">%</div>
      <div @click="divide" class="btn operator">&divide;</div>
      <div @click="append('7')" class="btn ">7</div>
      <div @click="append('8')" class="btn ">8</div>
      <div @click="append('9')" class="btn ">9</div>
      <div @click="times" class="btn times operator">&times;</div>
      <div @click="append('4')" class="btn ">4</div>
      <div @click="append('5')" class="btn ">5</div>
      <div @click="append('6')" class="btn ">6</div>
      <div @click="minus" class="btn minus operator">-</div>
      <div @click="append('1')" class="btn ">1</div>
      <div @click="append('2')" class="btn ">2</div>
      <div @click="append('3')" class="btn ">3</div>
      <div @click="plus" class="btn plus operator">+</div>
      <div @click="append('0')" class="btn zero">0</div>
      <div @click="dot" class="btn dot">.</div>
      <div @click="equal" class="btn equal operator">=</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        current: '',
        operator: null,
        previous: null,
        operatorEvent: false,
      };
    },
    methods: {
      clear() {
        this.current = '';
      },
      sign() {
        this.current =
          this.current.charAt(0) === '-'
            ? this.current.slice(1)
            : `-${this.current}`;
      },
      percent() {
        this.current =
          this.current != 0 ? `${parseFloat(this.current) / 100}` : '0';
      },
      append(number) {
        if (this.operatorEvent) {
          this.current = '';
          this.operatorEvent = false;
        }
        this.current = `${this.current}${number}`;
      },
      setPrevious() {
        this.previous = this.current;
        this.operatorEvent = true;
      },
      plus() {
        this.operator = (a, b) => a + b;
        this.setPrevious();
      },
      minus() {
        this.operator = (a, b) => a - b;
        this.setPrevious();
      },
      times() {
        this.operator = (a, b) => a * b;
        this.setPrevious();
      },
      divide() {
        this.operator = (a, b) => a / b;
        this.setPrevious();
      },
      dot() {
        if (this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },
      equal() {
        this.current = `${this.operator(
          parseFloat(this.current),
          parseFloat(this.previous)
        )}`;
        this.previous = null;
      },
    },
  };
</script>

<style>
@import '../assets/css/style.css';
</style>
