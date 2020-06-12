<template>
  <div class ="calculator">
    <div class="prev">{{ previous || '' }} {{ sign }}</div>
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn operator">C</div>
    <div @click="del" class="btn operator">Del</div>
    <div @click="percent" class="btn operator">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="mul" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="sub" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
      sign: '',
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    del() {
      if(this.current)
        this.current = this.current.slice(0, -1)
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if(number == '0' && this.current == '')
        this.current = ''
      else {
      if (this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
      }
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
      this.sign = '/'
      
    },
    mul() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
      this.sign = '*'
    },
    sub() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
      this.sign = '-'
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
      this.sign = '+'
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
        this.previous = null;
    }
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {

  grid-column: 1 / 5;
  background-color: white;
  border: 1px solid #333;
}
.prev {
   grid-column: 1 / 5;
  background-color: white;
  border: 1px solid #333;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: white;
  border: 1px solid #333;
}
.operator {
  background-color: white;
  color: orange;
}
</style>
