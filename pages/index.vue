<template>
    <div class="w-screen h-screen bg-slate-100 flex py-8 justify-center overflow-auto">
        <div class="bg-white p-8 rounded-lg shadow-lg flex flex-col h-fit w-full max-w-5xl">
            <h1 class="text-2xl flex justify-between font-semibold">Pacientes
                <NuxtLink to="/novo" class="bg-blue-500 plus hover:bg-blue-400 leading-none transition-all w-10 h-10 flex itens-center justify-center rounded-full text-2xl font-bold text-white"></NuxtLink>
            </h1>
            <PatientsCards />
        </div>
    </div>
</template>

<script lang="ts" setup>

const pacientes = ref([])

// Função para restaurar os dados do localStorage
function loadFromLocalStorage() {
    const savedData = localStorage.getItem('pacientes');
    if (savedData) {
        pacientes.value = JSON.parse(savedData)
    }
}

onMounted(loadFromLocalStorage);

</script>

<style>
.plus {
    background-image: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjExIiBoZWlnaHQ9IjIxMSIgdmlld0JveD0iMCAwIDIxMSAyMTEiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxwYXRoIGQ9Ik05Ny4yNjU2IDIxMC41NDdWMTEzLjA4NkgwVjk3LjA3MDNIOTcuMjY1NlYwSDExMi44OTFWOTcuMDcwM0gyMTAuNTQ3VjExMy4wODZIMTEyLjg5MVYyMTAuNTQ3SDk3LjI2NTZaIiBmaWxsPSJ3aGl0ZSIvPgo8L3N2Zz4K);
    background-size: 18px;
    background-repeat: no-repeat;
    background-position: center;
}
</style>