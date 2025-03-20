<script setup>
    const props = defineProps(["tarefasPendentes"]);
</script>

<template>
    <header>
        <h1>Minhas Tarefas</h1>
        <p>
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>