<template>
    <div class="flex flex-col gap-6 py-4">
        <div v-for="paciente in pacientes" :key="paciente.id" class="bg-white p-6 rounded-lg shadow-lg border border-gray-200 hover:shadow-xl transition-shadow duration-300">
            <h3 class="text-xl font-semibold text-gray-800">{{ paciente.nome }}</h3>
            <div class="mt-2">
                <p class="text-sm text-gray-600"><strong>Idade:</strong> {{ paciente.idade }} Anos</p>
                <p class="text-sm text-gray-600"><strong>Pressão: </strong> {{ paciente.pressaoSistolica }}/{{ paciente.pressaoDiastolica }} mmHg</p>
                <p class="text-sm text-gray-600"><strong>FC:</strong> {{ paciente.fc }} BPM</p>
                <p class="text-sm text-gray-600"><strong>FR:</strong> {{ paciente.fr }} MPM</p>
                <p class="text-sm text-gray-600"><strong>Temperatura:</strong> {{ paciente.temp }} ºC</p>
                <p class="text-sm text-gray-600"><strong>Oxigenação:</strong> {{ paciente.oxigenacao }}%</p>
                <p class="text-sm text-gray-600"><strong>Dextro:</strong> {{ paciente.dextro }} mg/dl</p>
                <p class="text-sm text-gray-600"><strong>Altura:</strong> {{ paciente.altura }} cm</p>
                <p class="text-sm text-gray-600"><strong>Peso:</strong> {{ paciente.peso }} kg</p>
                <p class="text-sm text-gray-600"><strong>Glasgow:</strong> {{ paciente.glasgow }}</p>
                <p class="text-sm text-gray-600"><strong>Deambula:</strong> {{ paciente.deambula == 'sim' ? 'Sim' : paciente.deambula == 'nao' ? 'Não' : 'Com Auxílio' }}</p>
                <p class="text-sm text-gray-600"><strong>Diurese:</strong> {{ paciente.diurese }}</p>
                <p class="text-sm text-gray-600"><strong>Evacuação:</strong> {{ paciente.evacuacao }}</p>
                <p class="text-sm text-gray-600"><strong>Alimentação:</strong> {{ paciente.alimentacao }}</p>
                <p class="text-sm text-gray-600"><strong>Admissão:</strong> {{ paciente.admissao }}</p>
                <p class="text-sm text-gray-600"><strong>Evolução:</strong> {{ paciente.evolucao }}</p>
            </div>
            <button @click="removePaciente(paciente.id)" class="mt-4 px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600 transition-colors duration-300">
                Remover Paciente
            </button>
        </div>
        <div v-if="pacientes.length === 0" class="text-center text-gray-500 text-lg">
            Nenhum paciente encontrado
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

// Estado para armazenar os dados dos pacientes
const pacientes = ref<any[]>([]);

// Função para carregar os dados do localStorage
function loadFromLocalStorage() {
    const savedData = localStorage.getItem('pacientes');
    if (savedData) {
        pacientes.value = JSON.parse(savedData);
    }
}

// Função para remover um paciente
function removePaciente(id: string) {
    // Filtra a lista para remover o paciente com o id especificado
    pacientes.value = pacientes.value.filter(paciente => paciente.id !== id);

    // Atualiza o localStorage com a nova lista
    localStorage.setItem('pacientes', JSON.stringify(pacientes.value));
}

// Carregue os dados ao montar o componente
onMounted(loadFromLocalStorage);
</script>

<style scoped>
/* O Tailwind CSS substitui as estilizações personalizadas */
</style>
