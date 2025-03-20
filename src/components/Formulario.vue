<script setup>
const props = defineProps(["cadastrarTarefa", "tarefaTemp", "trocarFiltro", "editaTarefaTemp"])
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa">
        <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" type="text"
            placeholder="Digite aqui a descrição da nova tarefa" required>
        <button type="submit">Cadastrar</button>
        <select @change="props.trocarFiltro">
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
        </select>
    </form>
</template>

<style>
button,
select {
    border-radius: 6px;
    cursor: pointer;
    text-align: center;
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
}

form button:hover {
    background-color: #5079ffc5;
}

form select {
    border: 1px solid #cdcdcd;
}
</style>