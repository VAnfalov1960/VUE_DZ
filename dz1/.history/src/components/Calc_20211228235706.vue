<template>
  <div class="calc">
    <h2>"Калькулятор ДЗ1"</h2>
    <button class="clear" @click="clear">Очистить</button>
    <input aria-label="op1" type="text" placeholder="Введите число" v-model.number="op1"/>
    <span>{{ operation }}</span>
    <input aria-label="op2" type="text" placeholder="Введите число" v-model.number="op2" /><br>
    <div class="result">
      <div>
        <h4>=</h4>
      </div>
      <div>
        <span v-if='Math.abs(result) < minmax' class="span">{{ result }}</span>
        <span v-if='Math.abs(result) > minmax' class="span">А поменьше числа можно? Спасибо.</span>
      </div>
    </div>
    <div class="btn">
      <button :hidden='op1 === "" || op2 === ""' @click="calculate('+')">+</button>
      <button :hidden='op1 === "" || op2 === ""' @click="calculate('-')">-</button>
      <button :hidden='op1 === "" || op2 === ""' @click="calculate('*')">*</button>
      <button :hidden='op1 === "" || op2 === "" || op2 === 0' @click="calculate('/')">/</button>
      <button :hidden='op1 === "" || op2 === ""' @click="step">Возвести в степень</button>
      <button :hidden='op1 === "" || op2 === "" || op2 === 0' @click="celdel">Целочисленное деление</button>
    </div>
    <h3 v-if='(op2 === 0)'>{{ errorText }}</h3>
  </div>
</template>

<script>

export default {
  name: 'Calc',
  data: () => ({
    minmax: 9007199254740991,
    operation: '',
    op1: '',
    op2: '',
    result: '',
    errorText: 'Внимание! На 0 делить нельзя!',
    buttons: ['+', '-', '*', '/', 'Возведение  в степень', 'Целочисленное деление']
  }),
  methods: {
    calculate (operation) {
      switch (operation) {
        case '+':
          this.add()
          break
        case '-':
          this.substract()
          break
        case '*':
          this.multiply()
          break
        case '/':
          this.divide()
          break
        case 'Возведение  в степень':
          this.step()
          break
        case 'Целочисленное деление':
          this.celdel()
          break
      }
    },
    clear () {
      this.op1 = ''
      this.op2 = ''
      this.operation = ''
      this.result = ''
    },
    add () {
      this.result = this.op1 + this.op2
    },
    substract () {
      this.result = this.op1 - this.op2
    },
    multiply () {
      this.result = this.op1 * this.op2
    },
    divide () {
      this.result = this.op1 / this.op2
    },
    step () {
      this.result = Math.pow(this.op1, this.op2)
    },
    celdel () {
      this.result = Math.floor(this.op1 / this.op2)
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.calc {
  width: 500px;
  min-height: 300px;
  margin-left: 50px;
  padding: 20px;
  border: 2px solid black;
  border-radius: 5px;
  background: rgba(252, 198, 5, .3);
  color: black;
}
h2 {
  margin: 0px;
  padding: 0px;
}
h3 {
  margin: 15px auto;
  color: white;
  border: 2px solid red;
  background: rgb(130, 16, 16);
  border-radius: 5px;
  width: 418px;
}
input {
  padding: 0px 5px 0px  5px ;
  width: 110px;
  height: 30px;
  margin: 20px;
  border: 2px solid black;
  border-radius: 5px;
  text-align: right;
}
.span {
  display: block;
  padding: 7px 5px 0 5px ;
  width: 370px;
  height: 30px;
  margin: 20px auto;
  border: 2px solid black;
  border-radius: 5px;
  background: white;
  text-align: right;
}
.result {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-around;
}
button {
  width: 200px;
  height: 40px;
  margin: 10px;
  border: 2px solid green;
  border-radius: 5px;
  background: grey;
  color: white;
}
button:hover {
  background: green;
  border: 2px solid black;
}
.btns {
  color: white;
}
.clear {
  width: 75px;
  height: 35px;
  margin: 10px;
  border: 2px solid black;
  border-radius: 5px;
  background: orangered;
  color: white;
}
.clear:hover {
  background: green;
  border: 2px solid orangered;
}
</style>
