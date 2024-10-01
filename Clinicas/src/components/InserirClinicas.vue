<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';   

const nome = ref<string>('');
const endereco = ref<string>('');
const cidade = ref<string>('');
const estado = ref<string>('');
const telefone = ref<string>('');
const email = ref<string>('');
const website = ref<string>('');


const inserirClinica = async () => {
  try {
    await axios.post('/clinicas', {
        id : 0,
        nome: nome.value,
        endereco: endereco.value,
        cidade: cidade.value,
        estado: estado.value,
        telefone: telefone.value,
        email: email.value,
        website: website.value,
    });
    alert('Dados enviados com sucesso!');
  } catch (error) {
    console.error('Erro ao inserir clínica:', error);
  }
};


</script>

<template>
    <div class="form-cadastrar">
      <form @submit.prevent="inserirClinica">
        <label for="nome">Nome:</label>
        <input v-model="nome" type="text" id="nome">
        <label for="endereco">Endereço:</label>
        <input v-model="endereco" type="text" id="endereco">
        <label for="cidade">Cidade</label>
        <input v-model="cidade" type="text" id="cidade">
        <label for="estado">Estado</label>
        <input v-model="estado" type="text" id="estado">
        <label for="telefone">Telefone</label>
        <input v-model="telefone" type="text" id="telefone">
        <label for="email">Email</label>
        <input v-model="email" type="text" id="email">
        <label for="website">Website</label>
        <input v-model="website" type="text" id="website">
        <button type="submit">Inserir</button>
      </form>
    </div>
</template>

<style scoped>

.form-cadastrar {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  width: 100%;
}

</style>