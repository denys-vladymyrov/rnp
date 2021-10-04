<template>
  <section class="flex flex-col max-w-xs p-6 items-start text-left">
    <label for="startInput">Enter arithmetic expression</label>
    <input type="text" id="startInput" class="form-input px-2 py-1" v-model.trim="expression"
           @input="incorrectExpression = false"
           @keyup.enter="inputKeyupHandler">
  </section>
</template>

<script>
  export default {
    name: 'App',
    data() {
      return {
        expression: '',
        resultToShow: '',
        globalStack: [],
        incorrectExpression: false
      }
    },
    methods: {
      inputKeyupHandler() {
        if (!this.checkCorrectInput()) {
          this.incorrectExpression = true;
          return;
        }
        const expr = this.expression.split(" ");

        if (expr.length === 1) {
          this.globalStack.push(expr[0]);

          this.expression = '';

          if (expr[0] === '+' ||
            expr[0] === '-' ||
            expr[0] === '*' ||
            expr[0] === "/"
          ) {
            this.showInConsole('<br>> ' + expr);
            this.calculate();
          } else {
            this.showInConsole('<br>> ' + expr + '<br>' + expr);
          }
        } else {
          this.calculate();
        }
      },
      showInConsole(text) {
        this.resultToShow += text;
      },
      checkCorrectInput() {
        const reg1 = /^[- + * //()]*[0-9][- + * //()0-9]*$/;
        const reg2 = /^[+\-*/]$/;

        if (this.expression === '') {
          return false;
        } else if (this.globalStack.length > 1 && reg2.test(this.expression)) {
          return true
        } else if (!reg1.test(this.expression)) {
          return false
        }
        return true;
      },
      calculate() {
        let expr = [];
        if (this.globalStack.length === 0 && this.expression !== '') {
          expr = this.expression.split(" ");
          this.showInConsole('<br>> ' + this.expression);
        } else if (this.globalStack.length !== 0 && this.expression !== '') {
          expr = [...this.globalStack, ...this.expression.split(" ")];
          this.showInConsole('<br>> ' + this.expression);
        } else {
          expr = this.globalStack;
        }

        this.expression = '';
        const stack = [];

        if (expr.length === 0) {
          return 0;
        }

        for (let i = 0; i < expr.length; i++) {
          if (!isNaN(parseInt(expr[i])) && isFinite(parseInt(expr[i]))) {
            stack.push(expr[i]);
          } else {
            let a = stack.pop();
            let b = stack.pop();

            switch (expr[i]) {
              case '+':
                stack.push(parseInt(a) + parseInt(b));
                break;
              case '-':
                stack.push(parseInt(b) - parseInt(a));
                break;
              case '*':
                stack.push(parseInt(a) * parseInt(b));
                break;
              case '/':
                stack.push(parseInt(b) / parseInt(a));
                break;
              default:
                console.log('error');
            }
          }
        }

        let result = null;
        if (stack.length > 1) {
          result = stack[stack.length - 1];
          this.resultToShow += '<br>' + result;
          this.globalStack.splice(this.globalStack.length - 3, 3);
          this.globalStack.push(result);
        } else {
          result = parseFloat(stack[0]);
          this.resultToShow += '<br>' + result;
          this.globalStack = [result];
        }
      }
    },
  }
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
</style>
