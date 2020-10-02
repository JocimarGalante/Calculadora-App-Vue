<template>
  <div>
    <h1>Calculadora</h1>
    <div class="col-2 my-1">
      <button
        v-on:click="mostrarCalculadora"
        type="button"
        class="btn btn-dark"
      >
        Modelo 1
      </button>
      <br />
      <br />
      <button v-on:click="mostrarModelo" type="button" class="btn btn-success">
        Modelo 2
      </button>
    </div>
    <div class="calculadora" v-if="mostrarNovo">
      <div class="display">{{ valorCorrente || "0" }}</div>
      <div v-on:click="limpar" class="botao">C</div>
      <div v-on:click="sinal" class="botao">+/-</div>
      <div v-on:click="porcentagem" class="botao">%</div>
      <div v-on:click="dividir" class="botao operadores">÷</div>
      <div v-on:click="juntarNumeros('7')" class="botao">7</div>
      <div v-on:click="juntarNumeros('8')" class="botao">8</div>
      <div v-on:click="juntarNumeros('9')" class="botao">9</div>
      <div v-on:click="multiplicar" class="botao operadores">x</div>
      <div v-on:click="juntarNumeros('4')" class="botao">4</div>
      <div v-on:click="juntarNumeros('5')" class="botao">5</div>
      <div v-on:click="juntarNumeros('6')" class="botao">6</div>
      <div v-on:click="diminuir" class="botao operadores">-</div>
      <div v-on:click="juntarNumeros('1')" class="botao">1</div>
      <div v-on:click="juntarNumeros('2')" class="botao">2</div>
      <div v-on:click="juntarNumeros('3')" class="botao">3</div>
      <div v-on:click="somar" class="botao operadores">+</div>
      <div v-on:click="juntarNumeros('0')" class="botao zero">0</div>
      <div v-on:click="ponto" class="botao">.</div>
      <div v-on:click="resultado" class="botao operadores">=</div>
    </div>
    <div class="calculator card col col-sm col-md" v-if="mostrar">
      <div class="calculator-screen z-depth-1">{{ valorCorrente || "0" }}</div>
      <div class="calculator-keys">
        <button type="button" class="operator btn btn-info" v-on:click="somar">
          +
        </button>
        <button
          type="button"
          class="operator btn btn-info"
          v-on:click="diminuir"
        >
          -
        </button>
        <button
          type="button"
          class="operator btn btn-info"
          v-on:click="multiplicar"
        >
          x
        </button>
        <button
          type="button"
          class="operator btn btn-info"
          v-on:click="dividir"
        >
          ÷
        </button>

        <button
          type="button"
          value="7"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('7')"
        >
          7
        </button>
        <button
          type="button"
          value="8"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('8')"
        >
          8
        </button>
        <button
          type="button"
          value="9"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('9')"
        >
          9
        </button>

        <button
          type="button"
          value="4"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('4')"
        >
          4
        </button>
        <button
          type="button"
          value="5"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('5')"
        >
          5
        </button>
        <button
          type="button"
          value="6"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('6')"
        >
          6
        </button>

        <button
          type="button"
          value="1"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('1')"
        >
          1
        </button>
        <button
          type="button"
          value="2"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('2')"
        >
          2
        </button>
        <button
          type="button"
          value="3"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('3')"
        >
          3
        </button>

        <button
          type="button"
          value="0"
          class="btn btn-light waves-effect"
          v-on:click="juntarNumeros('0')"
        >
          0
        </button>
        <button
          type="button"
          class="decimal function btn btn-secondary"
          v-on:click="ponto"
        >
          .
        </button>
        <button
          type="button"
          class="all-clear function btn btn-danger btn-sm"
          v-on:click="limpar"
        >
          AC
        </button>

        <button
          type="button"
          class="equal-sign operator btn btn-default"
          v-on:click="resultado"
        >
          =
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valorCorrente: "",
      valorSoma: "+",
      valorDiminui: "-",
      valorMultiplicar: "x",
      valorDividir: "÷",
      numeroAnterior: null,
      operador: null,
      operadorClicado: false,
      mostrar: false,
      mostrarNovo: false,
    };
  },
  methods: {
    mostrarCalculadora() {
      this.mostrar = true;
      this.mostrarNovo = false;
    },
    mostrarModelo() {
      this.mostrarNovo = true;
      this.mostrar = false;
    },
    limpar() {
      this.valorCorrente = "";
    },
    sinal() {
      this.valorCorrente =
        this.valorCorrente.charAt(0) === "-"
          ? this.valorCorrente.slice(1)
          : `-${this.valorCorrente}`;
    },
    porcentagem() {
      this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
    },
    juntarNumeros(numero) {
      if (this.operadorClicado) {
        this.valorCorrente = "";
        this.operadorClicado = false;
      }
      this.valorCorrente = `${this.valorCorrente}${numero}`;
    },
    ponto() {
      if (this.valorCorrente.indexOf(".") === -1) {
        this.juntarNumeros(".");
      }
    },
    setarValor() {
      this.numeroAnterior = this.valorCorrente;
      this.operadorClicado = true;
    },
    resultado() {
      this.valorCorrente = `${this.operador(
        parseFloat(this.numeroAnterior),
        parseFloat(this.valorCorrente)
      )}`;
      this.numeroAnterior = null;
    },
    dividir() {
      this.operador = (num1, num2) => num1 / num2;
      this.setarValor();
    },
    multiplicar() {
      this.operador = (num1, num2) => num1 * num2;
      this.setarValor();
    },
    diminuir() {
      this.operador = (num1, num2) => num1 - num2;
      this.setarValor();
    },
    somar() {
      this.operador = (num1, num2) => num1 + num2;
      this.setarValor();
    },
  },
};
</script>

<style scoped>
html {
  font-size: 62.5%;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

.calculator {
  border: 1px solid #ccc;
  border-radius: 5px;
  /* position: absolute; */
  margin: 0 auto;
  /* top: 50%;
      left: 50%; */
  /* transform: translate(-50%, -50%); */
  width: 400px;
}

.calculator-screen {
  width: 100%;
  height: 80px;
  border: none;
  background-color: #252525;
  color: #fff;
  text-align: right;
  padding-right: 20px;
  padding-left: 10px;
  font-size: 4rem;
}

button {
  height: 60px;
  font-size: 2rem !important;
}

.equal-sign {
  height: 98%;
  grid-area: 2 / 4 / 6 / 5;
  background-color: #2bbbad !important;
  color: #fff;
}
.equal-sign:hover {
  height: 98%;
  grid-area: 2 / 4 / 6 / 5;
  background-color: #269e92 !important;
  color: #fff;
}

.calculator-keys {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
  padding: 20px;
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.btn {
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12);
  /* padding: .84rem 2.14rem; */
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1 / 3;
}
.botao {
  background-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
}
.operadores {
  background-color: orange;
  color: white;
}
.calculadora {
  margin: 0 auto;
  width: 350px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
}
</style>
