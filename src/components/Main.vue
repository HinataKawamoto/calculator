<template>
  <div class="main">
    <div class="calculator">
      <div class="result" style="grid-area: result">{{ num }}</div>
      <button style="grid-area: percent" @click="percent()">%</button>
      <button style="grid-area: ce" @click="clear">CE</button>
      <button style="grid-area: c">C</button>
      <button style="grid-area: AC">AC</button>
      <button style="grid-area: _x">1/x</button>
      <button style="grid-area: _square">x²</button>
      <button style="grid-area: radical">2√x</button>
      <button style="grid-area: division" @click="append('/')">÷</button>
      <button style="grid-area: number7" @click="append(7)">7</button>
      <button style="grid-area: number8" @click="append(8)">8</button>
      <button style="grid-area: number9" @click="append(9)">9</button>
      <button style="grid-area: multiple" @click="append('*')">*</button>
      <button style="grid-area: number4" @click="append(4)">4</button>
      <button style="grid-area: number5" @click="append(5)">5</button>
      <button style="grid-area: number6" @click="append(6)">6</button>
      <button style="grid-area: minus" @click="append('-')">-</button>
      <button style="grid-area: number1" @click="append(1)">1</button>
      <button style="grid-area: number2" @click="append(2)">2</button>
      <button style="grid-area: number3" @click="append(3)">3</button>
      <button style="grid-area: plus" @click="append('+')">+</button>
      <button style="grid-area: pam">+/-</button>
      <button style="grid-area: number0" @click="append(0)">0</button>
      <button style="grid-area: point" @click="append('.')">.</button>
      <button class="equal" style="grid-area: equal" @click="calculate()">
        =
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num: 0,
    };
  },
  methods: {
    append(e) {
      console.log(e);
      if (this.num === 0) {
        this.num = "";
        if (e === ".") {
          this.num += "" + e;
        } else {
          this.num = "" + e;
        }
      } else {
        this.num += "" + e;
      }
    },
    calculate() {
      let result = this.num
        .replace(new RegExp("×", "g"), "*")
        .replace(new RegExp("÷", "g"), "/");
      this.num = parseFloat(eval(result).toFixed(9)).toString();
    },
    percent() {
      this.num = this.num + "* 0.01";
      this.calculate();
    },
    clear() {
      this.num = "0";
    },
  },
};
</script>

<style scoped lang="less">
.main {
  position: relative;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 322px;
  height: 564px;
  background-color: rgb(243, 243, 243);
}
.calculator {
  --button-width: 80px;
  --button-height: 70px;
  display: grid;
  grid-template-areas:
    "result result result result"
    "result result result result"
    "percent ce c AC"
    "_x _square radical division"
    "number7 number8 number9 multiple"
    "number4 number5 number6 minus"
    "number1 number2 number3 plus"
    "pam number0 point equal";
  grid-template-columns: repeat(4, var(--button-width));
  grid-template-rows: repeat(8, var(--button-height));
}
button {
  margin: 1px;
  background-color: #fff;
  border-radius: 7px;
  border: none;
  outline: none;
}
button:hover {
  background-color: rgb(252, 252, 252);
}
.result {
  position: absolute;
  right: 0;
  top: 70px;
  text-align: right;
  font-size: 30px;
}
.equal {
  background-color: rgb(0, 103, 192);
  color: white;
}

.equal:hover {
  background-color: rgb(25, 117, 197);
}
</style>