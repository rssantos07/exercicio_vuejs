<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'


const estado = reactive({
  valorATemp: '',
  valorBTemp: '',
  resultado: '',
  operacao: '',
  operador: [
    {
      operacao: 'Multiplicacao',
    },
    {
      operacao: 'Adição',
    },
    {

      operacao: 'Subtração',
    },
    {

      operacao: 'Divisão',
    },
    {

      operacao: 'Porcentagem',
    },
  ],

})

const multiplica = () => {
  estado.resultado = estado.valorATemp * estado.valorBTemp
  return estado.resultado
}

const soma = () => {
  const valorA = parseFloat(estado.valorATemp);
  const valorB = parseFloat(estado.valorBTemp);
  estado.resultado = valorA + valorB;
  return estado.resultado
}

const subtrai = () => {
  estado.resultado = estado.valorATemp - estado.valorBTemp
  return estado.resultado
}

const dividir = () => {
  estado.resultado = estado.valorATemp / estado.valorBTemp
  return estado.resultado
}

const porcento = () => {
  estado.resultado = (estado.valorBTemp * estado.valorATemp) / 100
  return estado.resultado
}

const limparCampos = () => {
    estado.valorATemp = '';
    estado.valorBTemp = '';
  }

const getOperacao = () => {
  const { operacao } = estado;
  switch (operacao) {
    case 'x':
      return multiplica();
    case '+':
      return soma();
    case '-':
      return subtrai();
      case '/':
      return dividir();
      case '%':
      return porcento();
      case '':
        return limparCampos();
      return ;
    default:
      return 0;
  }
}

</script>

<template>
  
  <div class="container">
    <Cabecalho/>
    <div class="col-md-12 text-center bg-dark mt-3 rounded-3 ">
      <h3 class="text-light p-4">Escolha a operação matemática antes de inserir os valores</h3>
      <form class="p-5 d-flex justify-content-evenly " >
        <input required type="number" placeholder="Valor A" :value="estado.valorATemp"  @keyup="evento => estado.valorATemp = evento.target.value">
        <h2 class="text-light">{{ estado.operacao }}</h2>
        <input required type="number" placeholder="Valor B" :value="estado.valorBTemp" @keyup="evento => estado.valorBTemp = evento.target.value">


        <div class="mb-5">
          <div class="col-12 text-light ">
            <select @change="evento => estado.operacao = evento.target.value" class="form-control">
              <option value="">Escolha a operação / Limpar</option>
              <option value="x">Multiplicação</option>
              <option value="+">Adição</option>
              <option value="-">Subtração</option>
              <option value="/">Divisão</option>
              <option value="%">Porcentagem</option>
            </select>
            

          </div>
        </div>
      </form>

      <div class=" col-12 text-light p-3">
          <h3>Resposta: {{ getOperacao() }}</h3>
      </div>
      
    </div>
  </div>
</template>

<style scoped></style>
