<template>
  <div class="wrapper">
    <div class="container">
      <div class="calculator__body">
        <div class="calculator__display"> 
          <span>{{ current  || 0 }}</span>
        </div>
        <div class="calculator__buttons">
          <div class="calculator__btn clear" v-on:click="clear">C</div>
          <div class="calculator__btn operator" v-on:click="sign">+/-</div>
          <div class="calculator__btn operator" v-on:click="percent">%</div>
          <div class="calculator__btn operator" v-on:click="divide">/</div>
          <div class="calculator__btn" v-on:click="append('8')">8</div>
          <div class="calculator__btn" v-on:click="append('7')">7</div>
          <div class="calculator__btn" v-on:click="append('9')">9</div>
          <div class="calculator__btn operator" v-on:click="multiply">X</div>
          <div class="calculator__btn" v-on:click="append('4')">4</div>
          <div class="calculator__btn" v-on:click="append('5')">5</div>
          <div class="calculator__btn" v-on:click="append('6')">6</div>
          <div class="calculator__btn operator" v-on:click="minus">-</div>
          <div class="calculator__btn" v-on:click="append('1')">1</div>
          <div class="calculator__btn" v-on:click="append('2')">2</div>
          <div class="calculator__btn" v-on:click="append('3')">3</div>
          <div class="calculator__btn operator" v-on:click="plus">+</div>
          <div class="calculator__btn zero" v-on:click="append('0')">0</div>
          <div class="calculator__btn" v-on:click="addDot">.</div>
          <div class="calculator__btn equal" v-on:click="equal">=</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props: {
    msg: String
  },
  data() {
    return {
      operator: null,
      previousNum: null,
      current: '',
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
    if(this.current.charAt(0) === '-') {
        this.current =  this.current.slice(1)
      } else {
        this.current = `-${this.current}`
      }
    },
    percent() {
      this.current = parseInt(this.current) / 100
    },
    append(num) {
      // if(this.current === '0') {
      //   this.current = ''
      // }
      if(this.operatorClicked) {
        this.current = ''
        this.operatorClicked = false
      }
      this.current = `${this.current}${num}`
    },
    addDot() {
       if (this.current === '0' || this.current === '-0') {
        this.current = this.current + '.'
      } else if(this.current.indexOf('.') === -1) {
        this.append('.')
       }
    },
    toPrevious() {
     
      this.previousNum = this.current 
      this.operatorClicked = true
    },  
    plus() {
      
      this.operator = (a, b) => a + b
      this.toPrevious()
    },
    minus() {
      this.operator = (a, b) => a - b
      this.toPrevious()
    },
    divide() {
      this.operator = (a, b) => a / b
      this.toPrevious()
    },
    multiply() {
      this.operator = (a, b) => a * b
      this.toPrevious()
    },
    equal() {
      this.current =  `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previousNum),
      )}`
      this.previousNum = null
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.wrapper {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
}
.container {
  max-width: 700px;
  margin: 0 auto;
}
.calculator {
		// .calculator__body
		&__body {
      overflow: hidden;
      max-width: 300px;
      font-size: 20px;
      margin-top: 70px;
      padding: 30px;
      background: #333333;
      border-radius: 15px;
      box-shadow: 10px 10px 0px #222121;
    }
		// .calculator__display
		&__display {
      text-align: right;
      padding: 5px;
      font-size: 35px;
      color: rgba(104,120,226,1);
      span {
        word-wrap: break-word;
      }
    }
		// .calculator__buttons
		&__buttons {
      display: grid;
      gap: 10px;
      grid-template-columns: repeat(4, 1fr);
    }
		// .calculator__btn
		&__btn {
      display: flex;
      justify-content:center;
      align-items: center;
      padding: 20px;
      cursor: pointer;
      color: #fff;
      font-weight: 700;
      // background: #ccc;
      transition: all 0.3s ease 0s;
      // box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.6);
      &:active {
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.8);
      }
    }
}
.clear {
  background: linear-gradient(90deg, rgba(104,120,226,1) 0%, rgba(224,72,71,1) 100%);
}
.operator {
  background: linear-gradient(90deg, rgba(104,120,226,1) 0%, rgba(116,81,171,1) 100%);

}
.equal {
  font-size: 30px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  color: #333333;
  background: linear-gradient(90deg, rgba(104,120,226,1) 0%, rgba(116,81,171,1) 100%);
}
.result {
  color: #ccc;
  font-size: 45px;
}

</style>
