<script setup>
  import { reactive } from "vue";

  const estado = reactive({
    filter: 'all',
    tarefaTemp: '',
    tarefas: [
      {titulo: "Estudar Vue", completed: false},
      {titulo: "Estudar ES6", completed: false},
      {titulo: "Estudar CSS", completed: false}
    ]
  })

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      completed: false
    }

    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = ''
  }

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefas => !tarefas.completed)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefas => tarefas.completed)
  }

  const getTarefasFiltradas = () => {
    const { filter } = estado;

    switch (filter) {
      case 'pending':
        return getTarefasPendentes();
      case 'completed':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }


</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendetes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Digite uma tarefa">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filter = evento.target.value" class="form-control">
            <option value="all">Todas as tarefas</option>
            <option value="completed">Concluidas</option>
            <option value="pending">Pendetes</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefas in getTarefasFiltradas()">
        <input @change="evento => tarefas.completed = evento.target.checked" :checked="tarefas.completed" :id="tarefas.titulo" type="checkbox">
        <label :class="{done: tarefas.completed === true}" class="ms-3" :for="tarefas.titulo">
          {{ tarefas.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
