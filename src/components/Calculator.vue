<template>
  <div class="calculator">
    <div class="display">{{ current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
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
			current: "",
			previous: null,
			operater: null,
			operaterClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      if (this.current !== "") {
        this.current =
          this.current.charAt(0) === "-"
            ? this.current.slice(1)
            : `-${this.current}`;
      }
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
			if (this.operaterClicked) {
				this.current = ''
				this.operaterClicked= false
			}
      if (this.current == "" && number == 0) {
        return;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
		},
		setPrevious() {
			this.previous = this.current
			this.operaterClicked = true
		},
		divide() {
			this.operater = (a, b) => a / b
			this.setPrevious()
		},
		times() {
			this.operater = (a, b) => a * b	
			this.setPrevious()	
		},
		subtract() {
			this.operater = (a, b) => a - b
			this.setPrevious()
		},
		add() {
			this.operater = (a, b) => a + b
			this.setPrevious()
		},
		equal() {
			this.current = `${this.operater(
				parseFloat(this.current),
				parseFloat(this.previous)
			)}`
			this.previous = null
		}
	}
}
</script>

<style>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(75px, auto);
  font-size: 30px;
  width: 350px;
  margin: 0 auto;
  font-family: "consolas";
  text-align: center;
  position:absolute;
    left:40%;
    top:10%;
}
.display {
  grid-column: 1 / 5;
  background-color: #1c1c1c;
  color: #fff;
  font-size: 70px;
  text-align: right;
  padding-right: 10px;
  height: 100px;
  padding-top: 30px;
}
.btn {
  background-color: #fff;
  color: #1c1c1c;
  border: 1px solid #d4d4d2;
  padding-top: 10px;
  cursor: pointer;
}
.operator {
  background-color: #ff9500;
  color: #fff;
}
.zero {
  grid-column: 1 / 3;
}
</style>