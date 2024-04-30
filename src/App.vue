<script setup>
import { reactive } from 'vue';

  const estado = reactive({  //CRIA O ESTADO E O ARRAY DE TAREFAS COM OBJETOS DAS TAREFAS
    filtro: '',  //MUDA O TITULO DA TAREFA EMBAIXO DO INPUT QUANDO TROCAMOS NO SELECT
    tarefaTemp: '',
    tarefas: [
      {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para a academia',
      finalizada: true,
    }
  ]
  }) 

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)  // FUNÇão QUE MUDA A QUANTIDADE DE TAREFAS NO <p> EM RELAÇÃO ÀS TAREFAS PENDENTES
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)  // do código 26 até o 41 fazemos funções para quando
  }                                                     //trocamos o valor do select do lado do botao aparecer as
                                                        //tarefas filtradas 
  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
        case 'finalizadas':
          return getTarefasFinalizadas()
          default:
            return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = ''; //após adicionar a tarefa ele limpa o campo do input
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} <!-- tarefas pendentes  essa função muda a quantidade de tarefas-->
      </p>                                              <!-- de acordo com quantas tarefas vc adicionou -->
    </header>
    <form @submit.prevent="cadastraTarefa"> <!-- o @submit faz o envio da nova tarefa cadastrada e o .prevent remova a ação de recarregar a página -->
      <div class="row">
        <div class="col">  <!-- com o value faz com que o input fique vazio após adicionar a tarefa -->
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>    <!-- Com esse @change fazemos o uso da função q criamos em scripts para cadastrar uma nova tarefa -->
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2"> <!-- O @CHANGE MUDA O TITULO DA TAREFA EMBAIXO DO INPUT QUANDO TROCAMOS NO SELECT -->
          <select @change="evento => estado.filtro = evento.target.value" class="form-control"> <!-- CRIA O CAMPO DO LADO DO BOTAO CADASTRAR-->
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    {{  estado.filtro }}
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()"> <!-- essa função faz aparecer apenas as tarefas, ou pendentes, ou finalizadas, ou todas as tarefas -->
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"> <!-- o @change muda o numero da quantidade de tarefas que nós possuimos quando nos clicamos no ckeckbox das tarefas disponiveis -->
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo"> <!-- FAZ A TAREFA FICAR COM O LINE-THROUGH QUANDO ESTIVER TRUE EM SCRIPTS -->
          {{ tarefa.titulo }}
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
