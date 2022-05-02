<template>
  <div class="container">
    <h1>Calculator</h1>
    <div class="display p-3">
      <div class="w-full">
        {{ currentValue || 0 }}
      </div>
    </div>
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div
          class="lead bg-success text-white m-1 py-3 rounded hover-class"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  props: {
    title: String,
  },
  data() {
    return {
      currentValue: "",
      operator: null,
      previousValue: "",
      calculatorElements: [
        "C",
        "()",
        "%",
        "/",
        1,
        2,
        3,
        "*",
        4,
        5,
        6,
        "-",
        7,
        8,
        9,
        "+",
        "+/-",
        0,
        ".",
        "=",
      ],
    };
  },
  methods: {
    action(n) {
      //>>Appending numbers in the screen
      if (!isNaN(n) || n === ".") {
        this.currentValue += n + "";
      }
      //clearig the screen
      if (n === "C") {
        this.currentValue = "";
      }
      if (n === "%") {
        this.currentValue = this.currentValue / 100 + "";
      }
      if (["+", "-", "*", "/"].includes(n)) {
        this.operator = n;
        this.previousValue = this.currentValue;
        this.currentValue = "";
      }
      if (n === "=") {
        this.currentValue = eval(
          this.previousValue + this.operator + this.currentValue
        );
        this.previousValue = "";
        this.operator = null;
      }
      if (n === "+/-") {
        this.currentValue = this.currentValue * -1;
      }
    },
    clear() {
      document.getElementById("current").innerHTML = "0";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.display {
  border-radius:10px;
  width: 100%;
  font-size: 2em;
  text-align: right;
  line-height: 40px;
  margin: 20px auto;
  max-width: 400px;
  background-color:slategrey;
  color: rgb(255, 255, 255);

}
.hover-class:hover {
  cursor: pointer;
}
.container {
  border-radius:10px;
  box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.7);
  max-width: 30rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding:1.5rem
}
</style>
