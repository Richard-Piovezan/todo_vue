<script setup>
    const props = defineProps(["tarefas"])
</script>

<template>
    <ul>
        <li v-for="tarefa in props.tarefas">
            <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo"
                type="checkbox">
            <label :class="{ done: tarefa.finalizada === true }" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style>
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