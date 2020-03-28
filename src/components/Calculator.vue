<template>
  <div class="calculator">
    <div class="display">{{ current || '0' }}</div>
    <div @click="clear" class="btn cancel">C</div>
    <div @click="sign" class="btn ">+/-</div>
    <div class="btn ">%</div>
    <div class="btn operator">/</div>
    <div class="btn ">7</div>
    <div class="btn ">8</div>
    <div class="btn ">9</div>
    <div class="btn star operator">*</div>
    <div class="btn ">4</div>
    <div class="btn ">5</div>
    <div class="btn ">6</div>
    <div class="btn minus operator">-</div>
    <div class="btn ">1</div>
    <div class="btn ">2</div>
    <div class="btn ">3</div>
    <div class="btn plus operator">+</div>
    <div class="btn zero">0</div>
    <div class="btn dot">.</div>
    <div class="btn equal operator">=</div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        current: '-1212',
      }
    },
    methods: {
      clear() {
        this.current = '';
      },
      sign() {
        this.current = this.current.charAt(0) === '-' ? this.current.slice(0) : `-${this.current}`
      }
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
