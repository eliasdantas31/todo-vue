<script setup>
  import { reactive } from 'vue';
  import Header from './componentes/Header.vue';
  import Form from './componentes/Form.vue';
  import List from './componentes/List.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar Vue',
        finalizada: false
      },
      {
        titulo: 'Estudar React',
        finalizada: false
      },
      {
        titulo: 'Estudar Angular',
        finalizada: false
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefas => !tarefas.finalizada); //! => === false
  }

  const getTarefasFinalizadas = () => {
      return estado.tarefas.filter(tarefas => tarefas.finalizada);
  }

  const getTarefasFiltradas = () => {
      const { filtro } = estado;

      switch (filtro) {
        case 'pendentes':
          return getTarefasPendentes();

        case 'finalizadas':
          return getTarefasFinalizadas();

        default:
          return estado.tarefas
      }
  }

  const cadastraTarefa = () => {
    // evento.preventDefault();

    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }
</script>

<template>
    <div class="container">
        <Header :tarefas-pendentes="getTarefasPendentes().length"></Header>
        <Form :trocar-filtro="evento => estado.filtro = evento.target.value" :cadastrar-tarefa="cadastraTarefa" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"></Form>
        <List :get-tarefas-filtradas="getTarefasFiltradas()"></List>
    </div>
</template>