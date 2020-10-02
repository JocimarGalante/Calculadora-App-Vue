<template>
  <div class="calculator card col col-sm col-md">
    <div class="calculator-screen z-depth-1">{{valorCorrente || '0'}}</div>
    <div class="calculator-keys">

      <button type="button" class="operator btn btn-info" v-on:click="somar">+</button>
      <button type="button" class="operator btn btn-info" v-on:click="diminuir">-</button>
      <button type="button" class="operator btn btn-info" v-on:click="multiplicar">x</button>
      <button type="button" class="operator btn btn-info" v-on:click="dividir">÷</button>

      <button type="button" value="7" class="btn btn-light waves-effect" v-on:click="juntarNumeros('7')">7</button>
      <button type="button" value="8" class="btn btn-light waves-effect" v-on:click="juntarNumeros('8')">8</button>
      <button type="button" value="9" class="btn btn-light waves-effect" v-on:click="juntarNumeros('9')">9</button>


      <button type="button" value="4" class="btn btn-light waves-effect" v-on:click="juntarNumeros('4')">4</button>
      <button type="button" value="5" class="btn btn-light waves-effect" v-on:click="juntarNumeros('5')">5</button>
      <button type="button" value="6" class="btn btn-light waves-effect" v-on:click="juntarNumeros('6')">6</button>


      <button type="button" value="1" class="btn btn-light waves-effect" v-on:click="juntarNumeros('1')">1</button>
      <button type="button" value="2" class="btn btn-light waves-effect" v-on:click="juntarNumeros('2')">2</button>
      <button type="button" value="3" class="btn btn-light waves-effect" v-on:click="juntarNumeros('3')">3</button>


      <button type="button" value="0" class="btn btn-light waves-effect" v-on:click="juntarNumeros('0')">0</button>
      <button type="button" class="decimal function btn btn-secondary" v-on:click="ponto">.</button>
      <button type="button" class="all-clear function btn btn-danger btn-sm" v-on:click="limpar">AC</button>

      <button type="button" class="equal-sign operator btn btn-default" v-on:click="resultado">=</button>

    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      valorCorrente: '',
      valorSoma: '+',
      valorDiminui: '-',
      valorMultiplicar: 'x',
      valorDividir: '÷', 
      numeroAnterior: null,
      operador: null,
      operadorClicado: false,
    };
  },
  methods:{
    limpar(){
      this.valorCorrente = '';
    },
    sinal(){
      this.valorCorrente = this.valorCorrente.charAt(0) === '-'
      ? this.valorCorrente.slice(1)
      : `-${this.valorCorrente}`;
    },
    porcentagem(){
      this.valorCorrente = `${parseFloat(this.valorCorrente)/100}`;
    },
    juntarNumeros(numero){
      if(this.operadorClicado){
        this.valorCorrente = '';
        this.operadorClicado = false;
      }
      this.valorCorrente = `${this.valorCorrente}${numero}`;
    },
    ponto(){
      if(this.valorCorrente.indexOf('.') === -1){
        this.juntarNumeros('.');
      }
    },
    setarValor(){
      this.numeroAnterior = this.valorCorrente;
      this.operadorClicado = true;
    },
    resultado(){
      this.valorCorrente = `${this.operador(
        parseFloat(this.numeroAnterior),
        parseFloat(this.valorCorrente),
      )}`;
      this.numeroAnterior = null;
    },
    dividir(){
      this.operador = (num1, num2) => num1 / num2;
      this.setarValor();
    },
    multiplicar(){
      this.operador = (num1, num2) => num1 * num2;
      this.setarValor();
    },
    diminuir(){
      this.operador = (num1, num2) => num1 - num2;
      this.setarValor();
    },
    somar(){
      this.operador = (num1, num2) => num1 + num2;
      this.setarValor();
    }
  }
  
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
      font-size: 2rem!important;
    }

    .equal-sign {
      height: 98%;
      grid-area: 2 / 4 / 6 / 5;
      background-color: #2bbbad!important;
      color: #fff;
    }
    .equal-sign:hover {
      height: 98%;
      grid-area: 2 / 4 / 6 / 5;
      background-color: #269e92!important;
      color: #fff;
    }

    .calculator-keys {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-gap: 20px;
      padding: 20px;
    }
.display{
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.btn{
  box-shadow: 0 2px 5px 0 rgba(0,0,0,.16), 0 2px 10px 0 rgba(0,0,0,.12);
  /* padding: .84rem 2.14rem; */
}

</style>