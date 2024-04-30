<script setup>
    const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas"> <!-- essa função faz aparecer apenas as tarefas, ou pendentes, ou finalizadas, ou todas as tarefas -->
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"> <!-- o @change muda o numero da quantidade de tarefas que nós possuimos quando nos clicamos no ckeckbox das tarefas disponiveis -->
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo"> <!-- FAZ A TAREFA FICAR COM O LINE-THROUGH QUANDO ESTIVER TRUE EM SCRIPTS -->
            {{ tarefa.titulo }}
        </label>
        </li>
        <li class="list-group-item" v-if="props.tarefas.filter(t => !t.finalizada).length === 0">
            Não existem tarefas pendentes
        </li>
    </ul>
</template>

<style scoped>
    .done {
    text-decoration: line-through;
    }
</style>