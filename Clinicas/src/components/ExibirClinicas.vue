<template>
    <div>

      <div v-if="dados.length > 0">
        <ul>
          <li v-for="(clinica, index) in dados" :key="index">
            <h2>{{ clinica.nome }}</h2>
            <p><strong>Endereço:</strong> {{ clinica.endereco }}</p>
            <p><strong>Cidade:</strong> {{ clinica.cidade }}</p>
            <p><strong>Estado:</strong> {{ clinica.estado }}</p>
            <p><strong>Telefone:</strong> {{ clinica.telefone }}</p>
            <p><strong>Email:</strong> {{ clinica.email }}</p>
            <p><strong>Website:</strong> {{ clinica.website }}</p>
            <hr />
          </li>
        </ul>
      </div>

      <div v-else class="dados-api-carregando">
        <p>Carregando dados...</p>
      </div>

    </div>
  </template>
  
  <script lang="ts" setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  // Variável reativa para armazenar os dados da API
  const dados = ref<Array<any>>([]); // Array para armazenar as clínicas
  
  // Função para fazer a requisição GET à API usando axios
  const buscarDados = async () => {
    try {
      const response = await axios.get('/clinicas');
      
      // Armazena os dados da resposta
      dados.value = response.data;
    } catch (error) {
      console.error('Erro ao buscar dados:', error);
    }
  };
  
  // Executar a função assim que o componente for montado
  onMounted(() => {
    buscarDados();
  });
  </script>
  
  <style scoped>
  .dados-api-carregando {
    text-align: center;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin-bottom: 20px;
  }
  </style>
  