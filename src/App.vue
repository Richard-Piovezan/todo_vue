<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  tarefas: [
    {
      titulo: "Estudar ES6",
      finalizada: false,
    },
    {
      titulo: "Estudar SASS",
      finalizada: false,
    },
    {
      titulo: "Ir para academia",
      finalizada: true,
    }
  ],

  filtro: "todas",
  tarefaTemporaria: '',
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false
  }

  if (tarefaNova.titulo.length >= 3) {
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemporaria = "";
  } else {
    alert("Por favor, especifique melhor sua tarefa\n\n(minímo de 3 caractéres)")
  }
}

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :tarefa-temp="estado.tarefaTemporaria" :edita-tarefa-temp="e => estado.tarefaTemporaria = e.target.value" :cadastrar-tarefa="cadastraTarefa" :trocar-filtro="e => estado.filtro = e.target.value" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>

<style scoped>
  * {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
    font-family: sans-serif;
    list-style: none;
  }

  body {
    min-width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .container {
    width: 80vw;
    margin: 0 auto;
  }

  header {
    padding: 80px;
    margin: 40px 0;
    background-color: #f5f5f5;
    border-radius: 16px;
  }

  header h1 {
    margin-bottom: 12px;
  }

  ul {
    margin-top: 30px;
    }
</style>
