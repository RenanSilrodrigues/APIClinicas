<script setup>
import { ref } from 'vue'; // Importando ref para reatividade
import axios from 'axios'; // Usando axios

// Criando variáveis reativas para a query de busca, os dados retornados e possíveis erros
const query = ref('');  // Termo de busca inicial
const data = ref(null);   // Dados retornados da API
const error = ref(null);  // Variável para armazenar erros

// Função para buscar os dados da API
const fetchData = async () => {
  error.value = null;  // Resetar o estado do erro antes da requisição
  try {
    console.log("Iniciando requisição com o nome:", query.value);  // Log de início de requisição
    const response = await axios.get('/clinicas/buscar', {
      params: { nome: query.value },
});
    console.log("Resposta recebida:", response.data);  // Log da resposta da API
    data.value = response.data;  // Atualizando os dados retornados
  } catch (err) {
    console.error('Erro ao buscar dados:', err);  // Log de erro
    error.value = err.message || 'Erro desconhecido';  // Atualizando a variável de erro para exibir no frontend
  }
};

</script>

<template>
    <div>
  
      <!-- Formulário de busca -->
      <form @submit.prevent="fetchData">
        <input v-model="query" placeholder="Busque por qualquer referencia" />
        <button type="submit">Buscar</button>
      </form>
  
      <!-- Exibindo o JSON retornado pela API -->
      <pre v-if="data">{{ data }}</pre>
  
      <!-- Exibindo mensagens de erro -->
      <p v-if="error" style="color: red;">Erro: {{ error }}</p>
    </div>
  </template>

<style scoped>

input {
  width: 93%;
}


</style>
  