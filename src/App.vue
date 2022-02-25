<template>
  <!-- 화면에 보여지는 영역 - html / hypertext markup language -->
  <div id="app">
    <!-- block, inline
    1. block - 태그가 전체 영역이 잡히는 것
    2. inine - 태그가 작성된 부분만 영역이 잡히는 것
    3. block > inline 
     -->

    <!-- block - div -->
    <!-- <div style="background-color: lightblue; width: 400px;">test</div> -->
    <!-- inline span -->
    <!-- <span style="background-color: orange; width: 400px;"> test </span> -->

    <input type="text" v-model="result" />

    <div>
      <div class="calculator-row">
        <div @click="clickNum(7)">7</div>
        <div @click="clickNum(8)">8</div>
        <div @click="clickNum(9)">9</div>
        <div @click="clickNum('/')">/</div>
      </div>

      <div class="calculator-row">
        <div @click="clickNum(4)">4</div>
        <div @click="clickNum(5)">5</div>
        <div @click="clickNum(6)">6</div>
        <div @click="clickNum('*')">*</div>
      </div>

      <div class="calculator-row">
        <div @click="clickNum(1)">1</div>
        <div @click="clickNum(2)">2</div>
        <div @click="clickNum(3)">3</div>
        <div @click="clickNum('-')">-</div>
      </div>

      <div class="calculator-row">
        <div @click="clickNum(0)">0</div>
        <div></div>
        <div class="result" @click="getResult">=</div>
        <div @click="clickNum('+')">+</div>
      </div>
    </div>
  </div>
</template>

<script>
// 화면에 보여지는 영역에 붙는 기능들 - javascript
export default {
  name: "App",

  data() {
    return {
      result: 0, // .bind()
      oneSet: [], // 0: num, 1: symbol, 2: num
    };
  },

  methods: {
    clickNum(num) {
      // isNaN = is not a number = 숫자가 아니니?
      let isSymbol = isNaN(num);

      if (this.oneSet.length === 0 && isSymbol === false) {
        this.oneSet.push(num);
      } else if (this.oneSet.length === 1 && isSymbol === true) {
        this.oneSet.push(num);
      } else if (this.oneSet.length === 2 && isSymbol === false) {
        this.oneSet.push(num);
      }
    },

    getResult() {
      switch (this.oneSet[1]) {
        case "/":
          this.result = this.oneSet[0] / this.oneSet[2];
          break;
        case "*":
          this.result = this.oneSet[0] * this.oneSet[2];
          break;
        case "-":
          this.result = this.oneSet[0] - this.oneSet[2];
          break;
        case "+":
          this.result = this.oneSet[0] + this.oneSet[2];
          break;
      }

      this.oneSet = [];
    },
  },
};
</script>

<style>
/* 화면에 보여지는 영역에 입히는 스타일(디자인/꾸미기) - css */

/* 우선순위
1. !important > inline > tag > class 
*/

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

/* class - html tag / css = . */
.calculator-row {
  display: flex;
}

.calculator-row div {
  background-color: #e3e3e3;
  width: 100px;
  height: 40px;
  line-height: 40px;
  margin: 5px;
  border-radius: 10px;
}

.calculator-row div:nth-child(4) {
  background-color: #aaaaaa;
}

.result {
  background-color: lightblue !important;
}

/* hover - css / over - javascript */
.calculator-row div:hover,
.result:hover {
  cursor: pointer;
  background-color: lightcoral !important;
}

input {
  width: 200px;
  height: 20px;
  margin: 0px 0px 20px 0px;
  text-align: right;
  font-size: 20px;
  border: 1px solid #bbbbbb;
  border-radius: 20px;
  padding: 10px;
}

/* .calculator-item {
  background-color: #e3e3e3;
  width: 100px;
  height: 40px;
  margin: 5px;
} */
</style>
