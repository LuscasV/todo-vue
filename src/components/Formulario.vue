<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa"> <!-- o @submit faz o envio da nova tarefa cadastrada e o .prevent remova a ação de recarregar a página -->
    <div class="row">
            <div class="col">  <!-- com o value faz com que o input fique vazio após adicionar a tarefa -->
        <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>    <!-- Com esse @change fazemos o uso da função q criamos em scripts para cadastrar uma nova tarefa -->
        <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2"> <!-- O @CHANGE MUDA O TITULO DA TAREFA EMBAIXO DO INPUT QUANDO TROCAMOS NO SELECT -->
            <select @change="props.trocarFiltro"> <!--CRIA O CAMPO DO LADO DO BOTAO CADASTRAR -->
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
            </select>
        </div>
        </div>
    </form>
</template>