<template>
  <div class="index">
    <h1>API Clinicas</h1>
    <div>
      <button @click="currentComponent = 'exibir'">Home</button>
      <button @click="currentComponent = 'inserir'">Cadastrar Clinica</button>
      <button @click="currentComponent = 'buscar'">Buscar Clinicas</button>
      <button @click="currentComponent = 'editar'">Editar Clinica</button>
      <button @click="currentComponent = 'excluir'">Excluir Clinica</button>
    </div>
    <div class="index-componet">
      <component :is="componentMap[currentComponent]"></component>  <!-- Componente dinâmico -->
    </div>
  </div>
</template>

<script lang="ts" setup>
// Importando os componentes
import { ref } from 'vue';

import BuscarClinicas from './components/BuscarClinicas.vue';
import ExibirClinicas from './components/ExibirClinicas.vue';
import InserirClinicas from './components/InserirClinicas.vue';
import EditarClinicas from './components/EditarClinicas.vue';
import ExcluirClinicas from './components/ExcluirClinicas.vue';


// Criando um mapa para associar as strings aos componentes reais
const componentMap = {
  exibir: ExibirClinicas,
  inserir: InserirClinicas,
  buscar: BuscarClinicas,
  editar: EditarClinicas,
  excluir: ExcluirClinicas,
};

// Definindo o componente inicial
const currentComponent = ref<keyof typeof componentMap>('exibir');
</script>

<style scoped>

.index {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 6vh;
}

.index-componet {
  max-height: 455px;
  min-width: 995px;
  overflow: auto;
  padding: 20px;
}

</style>
