<script setup>
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import Resultado from "./components/Resultado.vue";

const estado = reactive({
  operacoes: {
    soma: (a, b) => a + b,
    subtracao: (a, b) => a - b,
    multiplicacao: (a, b) => a * b,
    divisao: (a, b) => a / b,
  },
  calculo: "soma",
  numero1: null,
  numero2: null,
  resultado: null,
});

const filtraCalculo = (evento) => {
  estado.calculo = evento.target.value;
  moduloCalculo(); // Recalcula o resultado automaticamente ao alterar a operação
};

const atualizaNumero1 = (valor) => {
  estado.numero1 = valor;
  moduloCalculo(); // Recalcula o resultado ao alterar o número 1
};

const atualizaNumero2 = (valor) => {
  estado.numero2 = valor;
  moduloCalculo(); // Recalcula o resultado ao alterar o número 2
};

const moduloCalculo = () => {
  const operacao = estado.operacoes[estado.calculo];
  if (operacao && estado.numero1 !== null && estado.numero2 !== null) {
    estado.resultado = operacao(Number(estado.numero1), Number(estado.numero2));
  }
};
</script>

<template>
  <div class="container">
    <Cabecalho />
    <Formulario
      :moduloCalculo="moduloCalculo"
      :filtraCalculo="filtraCalculo"
      :estado1="estado.numero1"
      :estado2="estado.numero2"
      @atualiza-numero1="atualizaNumero1"
      @atualiza-numero2="atualizaNumero2"
    />
    <Resultado :estado="estado.resultado" />
  </div>
</template>

<style scoped></style>
