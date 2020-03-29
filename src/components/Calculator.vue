<template>
  <div class="calculator">
    <div class="display">{{ current || '0' }}</div>
    <div @click="clear" class="btn cancel">C</div>
    <div @click="sign" class="btn ">+/-</div>
    <div @click="percent" class="btn ">%</div>
    <div @click="devide" class="btn operator">/</div>
    <div @click="append('7')" class="btn ">7</div>
    <div @click="append('8')" class="btn ">8</div>
    <div @click="append('9')" class="btn ">9</div>
    <div @click="star" class="btn star operator">*</div>
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
</template>

<script>
  export default {
    data() {
      return {
        current: '',
        operator: null,
        previous: null,
        operatorEvent: false,
      }
    },
    methods: {
      clear() {
        this.current = '';
      },
      sign() {
        this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
      },
      percent() {
        this.current = `${parseFloat(this.current) / 100}`;
      },
      append(number) {
        if(this.operatorEvent) {
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
      star() {
        this.operator = (a, b) => a * b;
        this.setPrevious();
      },
      devide() {
        this.operator = (a, b) => a / b;
        this.setPrevious();
      },
      dot() {
        if(this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },
      equal() {
        this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`;
        this.previous = null;
      },
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .calculator {
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    display: grid;
    font-size: 40px;
    width: 400px;
    margin: 0 auto;
  }
  .display {
    grid-column: 1 / 5;
    background-color: #333333;
    color: #ffffff;
  }
  .btn {
    background-color: #f2f2f2;
    cursor: pointer;
    border: 1px solid #999999;
  }
  .btn:selected, .btn:focus {
    color: blue;
  }
  .zero {
    grid-column: 1 / 3;
  }
  .operator {
    background-color: orange;
    color: #ffffff;
  }
</style>
