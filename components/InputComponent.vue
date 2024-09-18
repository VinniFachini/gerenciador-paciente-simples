<template>
    <div class="w-full">
        <label :for="inputId" class="block text-sm text-gray-500">{{ label }}</label>
        <input :type="type" :id="inputId" :value="inputValue" :required="required" v-model="inputValue" :placeholder="placeholder" @input="$emit('update:modelValue', $event.target.value)" class="block mt-2 w-full placeholder-gray-400/70  rounded-lg border border-gray-200 bg-white px-5 py-2.5 text-gray-700 focus:border-blue-400 focus:outline-none focus:ring focus:ring-blue-300 focus:ring-opacity-40  " />
    </div>
</template>

<script setup lang="ts">
import { ref, computed, watch } from 'vue';

const props = defineProps<{
    id: string;
    label: string;
    placeholder: string;
    type: string;
    required: boolean
}>();

const inputValue = ref('');
const inputId = computed(() => props.id || 'UserInput');

</script>

<style scoped>
/* Adicione seus estilos aqui */
</style>