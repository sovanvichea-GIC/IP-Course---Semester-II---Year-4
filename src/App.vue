<template>
  <div id="app">
    <div class="container">
      <table>
        <tr>
          <td colspan="5">
            <div id="screen">
              <span id="screen_top">M=0</span>
              <div id="screen_bottom">
                <!-- v-text is a directive that is used to replace the content of HTML tag with private data -->
                <!-- It will update the content automatically when data is changed. It is called data reactive -->
                <span v-text="inputNumber" id="operand1">0</span>
                <span id="operator"></span>
                <span id="operand2"></span>
              </div>
              <!-- <span id="screen_bottom">0</span> -->
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-warning">MC</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning">MR</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning">M-</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning">M+</button>
          </td>
          <td>
            <button
              v-on:click="deleteOneNumber()"
              type="button"
              class="btn btn-light"
            >
              <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
            </button>
          </td>
        </tr>
        <tr>
          <td>
            <button
              v-on:click="showNumber(7)"
              type="button"
              class="btn btn-light"
            >
              7
            </button>
          </td>
          <td>
            <button
              v-on:click="showNumber(8)"
              type="button"
              class="btn btn-light"
            >
              8
            </button>
          </td>
          <td>
            <button
              v-on:click="showNumber(9)"
              type="button"
              class="btn btn-light"
            >
              9
            </button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary">÷</button>
          </td>
          <td>
            <button type="button" class="btn btn-light">+/-</button>
          </td>
        </tr>
        <tr>
          <td>
            <button
              v-on:click="showNumber(4)"
              type="button"
              class="btn btn-light"
            >
              4
            </button>
          </td>
          <td>
            <button
              v-on:click="showNumber(5)"
              type="button"
              class="btn btn-light"
            >
              5
            </button>
          </td>
          <td>
            <button
              v-on:click="showNumber(6)"
              type="button"
              class="btn btn-light"
            >
              6
            </button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary">x</button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary">-</button>
          </td>
        </tr>
        <tr>
          <td>
            <button
              v-on:click="showNumber(1)"
              type="button"
              class="btn btn-light"
            >
              1
            </button>
          </td>
          <td>
            <button
              v-on:click="showNumber(2)"
              type="button"
              class="btn btn-light"
            >
              2
            </button>
          </td>
          <td>
            <button
              v-on:click="showNumber(3)"
              type="button"
              class="btn btn-light"
            >
              3
            </button>
          </td>
          <td rowspan="2">
            <button type="button" class="btn btn-secondary long-btn">+</button>
          </td>
          <td rowspan="2">
            <button type="button" class="btn btn-primary long-btn">=</button>
          </td>
        </tr>
        <tr>
          <td>
            <button
              v-on:click="deleteAll()"
              type="button"
              class="btn btn-danger"
            >
              C
            </button>
          </td>
          <td>
            <button
              v-on:click="showNumber(0)"
              type="button"
              class="btn btn-light"
            >
              0
            </button>
          </td>
          <td>
            <button
              v-on:click="pointNumber()"
              type="button"
              class="btn btn-light"
            >
              .
            </button>
          </td>
        </tr>
      </table>
    </div>
    <div class="alert alert-danger" id="message_panel" role="alert">
      something wrong here
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      // This is the private data section which can be used inside this component
      inputNumber: 0,
      operand1:0,
    };
  },
  methods: {
    showNumber(number) {
       
      // Assign number when user click to the inputNumber data
      // To access private data from methods, use (this.)
    if (this.inputNumber.length > "14") {
        alert("Can not input more number !!!");
        this.inputNumber = this.inputNumber.slice(0, this.inputNumber.length-1)
      }

     // console.log("Length Digit: "+this.inputNumber.length);

     // console.log(number);
      number = this.inputNumber + number.toString();
      this.inputNumber = number;
      //console.log(number);

     
      if (this.inputNumber[0] == "0" && this.inputNumber.indexOf(".") == -1) {
       // console.log("true");
        this.inputNumber = this.inputNumber.slice(1);
      }

      this.operation1 = parseFloat(this.inputNumber);
      console.log("NumberDisplay = " + this.inputNumber);
      console.log("operation1 = " + this.operation1);
      console.log("");
    },

    pointNumber(){

      if(this.inputNumber == "0"){
        this.showNumber(0);
        this.inputNumber = this.inputNumber + ".";
        console.log("NumberDisplay = 0.")
        console.log("operation1 = " + this.operation1);
        console.log("");
        
      }else if(this.inputNumber.indexOf(".") > -1 ){
        this.inputNumber = this.inputNumber + "";
      }else{
        this.inputNumber = this.inputNumber + ".";
        console.log("NumberDisplay = " + this.inputNumber)
        this.operation1 = parseFloat(this.inputNumber);
        console.log("operation1 = " + this.operation1);
        console.log("");
      }
     
    },

    deleteAll() {
      this.inputNumber = 0;
      console.log("clear");
      console.log("");
    },

    deleteOneNumber() {
      console.log(this.inputNumber);
     if(this.inputNumber.length <= 1){
        this.inputNumber = 0;
      }else if(this.inputNumber.length > 0){
        this.inputNumber = this.inputNumber.slice(0, this.inputNumber.length - 1);
      }
    },

  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  margin-top: 10em;
  width: 300px;
  border: 1px solid black;
  padding-top: 20px;
  padding-bottom: 20px;
}
table {
  border-spacing: 7px;
  border-collapse: separate;
}
#screen {
  border: 1px solid black;
  padding: 7px;
  width: 100%;
  height: 4em;
}
#screen_top {
  display: block;
  font-size: 0.8rem;
}
#screen_bottom {
  font-size: 1.8rem;
  display: block;
  text-align: right;
}
#operand2 {
  background-color: skyblue;
}
#operator {
  background-color: rosybrown;
}
.button-row {
  display: flex;
  justify-content: space-between;
}
button {
  width: 45px;
}
.long-btn {
  display: inline-block;
  height: 80px;
}

/* Message panel */
#message_panel {
  width: 300px;
  margin-top: 1em;
  display: none;
  margin-left: auto;
  margin-right: auto;
}
</style>
