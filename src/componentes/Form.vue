<script setup>
    const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTEmp']);
</script>
<template>
    <form @submit.prevent="props.cadastrarTarefa">
        <div class="row">
          <div class="col">
            <input :value="props.tarefaTemp" @change="props.editaTarefaTEmp" required type="text" placeholder="digite aqui a descrição da tarefa" class="form-control">
          </div>
          <div class="col-md-1">
            <button type="submit" class="btn btn-primary">Adicionar</button>
          </div>
          <div class="col-md-2">
            <select @change="props.trocarFiltro" class="form-control">
              <option value="todas">Todas as Tarefas</option>
              <option value="pendentes">Pendentes</option>
              <option value="finalizadas">Finalizadas</option>
            </select>
          </div>
        </div>
    </form>    
</template>