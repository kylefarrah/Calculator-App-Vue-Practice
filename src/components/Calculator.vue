<template>
  <div id="calculator">
    <h1 id="outputBox">
      {{ currentNumber }}
    </h1>
    <div class="row">
    <div class="calculatorNum col-sm-3 btn" @click="clear">C</div>
    <div class="calculatorNum col-sm-3 btn" @click="sign">+/-</div>
    <div class="calculatorNum col-sm-3 btn" @click="operation('exp')">x^y</div>
    <div class="operator col-sm-3 btn" @click="operation('divide')">/</div>
  </div>
  <div class="row">
    <div class="calculatorNum col-sm-3 btn" @click="append('7')">7</div>
    <div class="calculatorNum col-sm-3 btn" @click="append('8')">8</div>
    <div class="calculatorNum col-sm-3 btn" @click="append('9')">9</div>
    <div class="operator col-sm-3 btn" @click="operation('times')">X</div>
  </div>
  <div class="row">
    <div class="calculatorNum col-sm-3 btn" @click="append('4')">4</div>
    <div class="calculatorNum col-sm-3 btn" @click="append('5')">5</div>
    <div class="calculatorNum col-sm-3 btn" @click="append('6')">6</div>
    <div class="operator col-sm-3 btn" @click="operation('subtract')">-</div>
  </div>
  <div class="row">
    <div class="calculatorNum col-sm-3 btn" @click="append('1')">1</div>
    <div class="calculatorNum col-sm-3 btn" @click="append('2')">2</div>
    <div class="calculatorNum col-sm-3 btn" @click="append('3')">3</div>
    <div class="operator col-sm-3 btn" @click="operation('add')">+</div>
  </div>
  <div class="row">
    <div class="calculatorNum col-sm-6 btn" @click="append('0')">0</div>
    <div class="calculatorNum col-sm-3 btn" @click="append('.')">.</div>
    <div class="operator col-sm-3 btn" @click="evaluate">=</div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {

  },
  data: function() {
return {
    currentNumber: "0",
    operatorType: "",
    previousNumber: "0"
  };
},
methods: {
  append(number) {
    if(this.currentNumber === "0"){
      this.currentNumber = number;
    }
    else{
      this.currentNumber = this.currentNumber + number;
    }
  },
  sign(){
    if(this.currentNumber[0] === "-"){
      this.currentNumber = this.currentNumber.substr(1);
    }
    else{
      this.currentNumber = "-" + this.currentNumber;
    }
  },
  clear(){
    this.previousNumber = "0";
    this.currentNumber = "0";
    this.operatorType = "";
  },
  operation(operationType){
    this.operatorType = operationType;
    this.previousNumber = this.currentNumber;
    this.currentNumber = "0";
  },
  evaluate(){
    if(this.operatorType === "times"){
      this.currentNumber = parseFloat(this.previousNumber) * parseFloat(this.currentNumber);
    }
    else if(this.operatorType === "divide"){
      this.currentNumber = parseFloat(this.previousNumber) / parseFloat(this.currentNumber);
    }
    else if(this.operatorType === "add"){
      this.currentNumber = parseFloat(this.previousNumber) + parseFloat(this.currentNumber);
    }
    else if(this.operatorType === "subtract"){
      this.currentNumber = parseFloat(this.previousNumber) - parseFloat(this.currentNumber);
    }
    else if(this.operatorType === "exp"){
      this.currentNumber = Math.pow(parseFloat(this.previousNumber), parseFloat(this.currentNumber));
    }

    this.currentNumber = Math.round(1000 * this.currentNumber)/1000;

    this.previousNumber = "0";
    this.operatorType = "";
    this.currentNumber = this.currentNumber.toString();
  }
}
}
</script>


<style scoped>
#calculator{
  width: 300px;
  margin: 0 auto;
}
#outputBox{
  background-color: #1C1C1C;
  color: #D4D4D4;
  width: 100%;
  height: 75px;
  text-align: right;
  padding-right: 10px;
  vertical-align: middle;
  display: inline-block;
  line-height: 75px;
  margin-bottom: 3px;
}
.row{
  width: 300px;
  margin: 0 auto;
}
.btn{
  border: 1px solid black;
  border-radius: 0px;
}
.calculatorNum{
  background-color: #505050;
  color: #D4D4D4;
}
.calculatorNum:active{
  background-color: black;
}
.operator{
  background-color: #FF9500;
}
.operator:active{
  background-color: black;
}
</style>
