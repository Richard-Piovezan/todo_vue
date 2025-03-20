<script setup>
    const props = defineProps(["tarefas"])
</script>

<template>
    <ul>
        <li v-if="props.tarefas.length === 0">
            <span class="pendentes_zeradas">
                Não existe tarefas pendentes!
            </span>
        </li>
        <li v-else v-for="tarefa in props.tarefas">
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

    .pendentes_zeradas {
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgba(47, 192, 103, 0.3);
        color: #207718;
        font-weight: bold;
        height: 40px;
    }
</style>