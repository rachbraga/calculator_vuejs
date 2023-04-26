<template>
 <div class="container">  
    <div class="result">
    <p>{{ numero || '0' }}</p>
  </div>
  <div class="calculator">
  <button @click="zerar" class="number light"> C </button>
  <button @click="mudarSinal" class="number light"> +/- </button>
  <button @click="porcentagem" class="number light"> % </button>
  <button @click="dividir" class="number sinal"> ÷ </button>
  <button @click="adicionarNumero('7')" class="number"> 7 </button>
  <button @click="adicionarNumero('8')" class="number"> 8 </button>
  <button @click="adicionarNumero('9')" class="number"> 9 </button>
  <button @click="multiplicar" class="number sinal"> x </button>  
  <button @click="adicionarNumero('4')" class="number"> 4 </button>
  <button @click="adicionarNumero('5')"  class="number"> 5 </button>
  <button @click="adicionarNumero('6')" class="number"> 6 </button>
  <button @click="diminuir" class="number sinal"> - </button>
  <button @click="adicionarNumero('1')" class="number"> 1 </button>
  <button @click="adicionarNumero('2')" class="number"> 2 </button>
  <button @click="adicionarNumero('3')" class="number"> 3 </button> 
  <button @click="somar" class="number sinal"> + </button>
  <button @click="adicionarNumero('0')" class="number igual"> 0 </button>
  <button @click="ponto" class="number"> . </button>  
  <button v-on:click="resultadoTotal" class="number sinal"> = </button>
</div>
 </div>  
</template>
<script>


export default {
  name: 'App', 
  data(){
    return {
      numero: '',
      numeroAnterior: null,
      op: null,
      opClicado:false,
      
    }
  },
  methods:{
    adicionarNumero(num){
      if(this.opClicado){
        this.numero = '';
        this.opClicado = false;
      } 
      this.numero = `${this.numero}${num}`      
    },   
    zerar(){
      this.numero = '';
    },
    mudarSinal(){
      this.numero = this.numero.charAt(0) === '-' ? this.numero.slice(1) : `-${this.numero}`;
    },
    porcentagem(){
      this.numero = `${parseFloat(this.numero)/100}`;
    },
    ponto(){
      if(this.numero.indexOf('.') === -1){
        this.adicionarNumero('.')
      }
    },
    setarValor(){
      this.numeroAnterior = this.numero;
      this.opClicado = true;
    },
    resultadoTotal(){
      this.numero = `${this.op(
        parseFloat(this.numeroAnterior),
        parseFloat(this.numero),
      )}`;
      this.numeroAnterior = null;
    },  
    dividir(){
      this.op = (num1,num2) => num1/num2;
      this.setarValor();
    },
    multiplicar(){
      this.op = (num1,num2) => num1*num2;
      this.setarValor();
    },
    diminuir(){
      this.op = (num1,num2) => num1-num2;
      this.setarValor();
    },
    somar(){
      this.op = (num1,num2) => num1+num2;
      this.setarValor();
    },
},
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display:flex;
  justify-content: center;
  align-content: center;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  display:flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  justify-content: flex-end;
  height: 430px;
  width: 225px;
  font-size: 28px;
  border-radius:15px;
  background-color: black;
}
.result{
  display:flex;
  justify-content: flex-end;
  align-items: flex-end;
  font-size: 45px;
  margin-right: 50px;
  color: white;
  width: 98%;
}

.number{
  padding: 12px;
  border: none;
  border-radius: 100%;
  background-color:rgb(31, 28, 30);
  
}
.calculator{
  margin-bottom:30px;
}
.igual{
  border-radius:40px;
  width:44%;
}
.sinal{
  background-color: #ddb120;  
}
.light{
  background-color: #858d85;
}
button{
  width: 50px;
  height: 50px;
  margin:2px;
  border: none;
  border-radius: 4px;
  background-color: #4caf50;
  color: #fff;
  font-size: 24px;
  cursor: pointer;
}
button:hover {
  background-color: rgba(141, 134, 134, 0.671);
}
</style>
