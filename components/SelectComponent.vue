<template>
    <div class="w-full">
        <label :for="selectId" class="block text-sm text-gray-500">{{ label }}</label>
        <select :id="selectId" v-model="selectedValue" class="block mt-2 w-full placeholder-gray-400/70  rounded-lg border border-gray-200 bg-white px-5 py-2.5 text-gray-700 focus:border-blue-400 focus:outline-none focus:ring focus:ring-blue-300 focus:ring-opacity-40  ">
            <option v-for="option in options" :key="option.value" :value="option.value">
                {{ option.label }}
            </option>
        </select>
    </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

const props = defineProps<{
    id: string;
    label: string;
    options: { value: string | number, label: string }[];
    modelValue: string | number;
}>();

const emit = defineEmits(['update:modelValue']);
const selectedValue = ref(props.modelValue);

// Atualiza o valor quando o usuário seleciona uma opção
watch(selectedValue, (newValue) => {
    emit('update:modelValue', newValue);
});

// Define um ID padrão caso não seja passado
const selectId = computed(() => props.id || 'UserSelect');
</script>

<style scoped>
/* Adicione seus estilos aqui */
</style>