<script setup>
  import { reactive, ref } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({  //CRIA O ESTADO E O ARRAY DE TAREFAS COM OBJETOS DAS TAREFAS
    filtro: '',  //MUDA O TITULO DA TAREFA EMBAIXO DO INPUT QUANDO TROCAMOS NO SELECT
    tarefaTemp: '',
    tarefas: [
    { titulo: 'Estudar ES6', finalizada: false, },
    { titulo: 'Estudar SASS', finalizada: false, },
    { titulo: 'Ir para a academia', finalizada: true, },
  ],
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
    <Cabecalho  :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


