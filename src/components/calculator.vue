<template>
  <div class="calculator">
      <div class="display">{{current || '0'}}</div>
      <div class="btn" @click='clear'>C</div>
      <div class="btn" @click='sign'>+/-</div>
      <div class="btn" @click='percent'>%</div>
      <div class="btn operator" @click='divide'>/</div>
      <div class="btn" @click='append("7")'>7</div>
      <div class="btn" @click='append("8")'>8</div>
      <div class="btn" @click='append("9")'>9</div>
      <div class="btn operator" @click='times'>x</div>
      <div class="btn" @click='append("4")'>4</div>
      <div class="btn" @click='append("5")'>5</div>
      <div class="btn" @click='append("6")'>6</div>
      <div class="btn operator" @click='minus'>-</div>
      <div class="btn" @click='append("1")'>1</div>
      <div class="btn" @click='append("2")'>2</div>
      <div class="btn" @click='append("3")'>3</div>
      <div class="btn operator" @click='add'>+</div>
      <div class="btn zero" @click='append("0")'>0</div>
      <div class="btn" @click='dot'>.</div>
      <div class="btn operator" @click='equal'>=</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      current: '0',
      operator: null,
      previous: null,
      operatorClicked: false
    }
  },
  methods: {
    clear () {
      this.current = ''
    },
    setPrevious () {
      this.previous = this.current
      this.operatorClicked = true
    },
    sign () {
      this.current = this.current * -1
    },
    percent () {
      this.current = `${parseFloat(this.current) / 100}`
      this.setPrevious()
    },
    append (number) {
      if (this.operatorClicked) {
        this.current = ''
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot () {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    divide () {
      this.operator = (a, b) => a / b
      this.setPrevious()
    },
    times () {
      this.operator = (a, b) => a * b
      this.setPrevious()
    },
    minus () {
      this.operator = (a, b) => a - b
      this.setPrevious()
    },
    add () {
      this.operator = (a, b) => a + b
      this.setPrevious()
    },
    equal () {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`
      this.previous = null
    }
  }
}
</script>

<style scoped>
.calculator{
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px,auto);
    font-size: 40px;
    width: 400px;
    margin: 0 auto;
}
.display{
    grid-column: 1/5;
    background-color: #333;
    color: #eee
}
.zero{
    grid-column: 1/3
}
.btn{
    background-color: #f2f2f2;
    border: 1px solid #333;
    cursor: pointer;
}
.operator{
    background-color: rgb(245, 177, 50);
    color: #eee
}
</style>
