<script setup>
import { reactive } from 'vue';

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
    <header>
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa()">
      <input :value="estado.tarefaTemporaria" @change="e => estado.tarefaTemporaria = e.target.value" type="text" placeholder="Digite aqui a descrição da nova tarefa" required>
      <button type="submit">Cadastrar</button>
      <select @change="e => estado.filtro = e.target.value">
        <option value="todas">Todas tarefas</option>
        <option value="pendentes">Pendentes</option>
        <option value="finalizadas">Finalizadas</option>
      </select>
    </form>
    <ul>
      <li v-for="tarefa in getTarefasFiltradas()">
        <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada === true }" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
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

  button, select {
    border-radius: 6px;
    cursor: pointer;
  }

  form {
    width: 100%;
    display: grid;
    grid-template-columns: 80% 8% 8%;
    gap: 2%;
  }

  form input {
    height: 36px;
    border-radius: 8px;
    border: 1px solid #cdcdcd;
    text-indent: 12px;
    font-size: 16px;
  }

  form button {
    background-color: #5079ff;
    border: none;
    color: #fff;
    font-weight: 100;
    transition: .3s;
  } form button:hover {
    background-color: #5079ffc5;
  }

  form select {
    border: 1px solid #cdcdcd;
  }

  ul {
    margin-top: 30px;
  }
  
  ul li {
    display: flex;
    align-items: center;
    padding: 10px 16px;
    border-radius: 6px;
    border: 1px solid #cdcdcd;
    font-size: 15px;
    margin-bottom: 8px;
  }

  ul li label {
    margin-left: 12px;
  }

  .done {
    text-decoration: line-through;
  }
</style>
