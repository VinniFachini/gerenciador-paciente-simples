<template>
    <div class="w-screen h-screen bg-slate-100 flex py-8 justify-center overflow-auto">
        <div class="bg-white p-8 rounded-lg shadow-lg flex flex-col h-fit w-full max-w-5xl">
            <div class="relative flex items-center justify-start gap-4">
                <NuxtLink to="/" class="go-back"></NuxtLink>
                <h1 class="text-2xl font-semibold pl-8">Adicionar Paciente</h1>
            </div>
            <form @submit.prevent="handleSubmit" class="flex items-start justify-start w-full flex-col">
                <!-- Campos do formulário -->
                <InputComponent required id="nome" label="Nome" type="text" placeholder="Nome do Paciente" v-model="form.nome" class="pt-4" />
                <InputComponent required id="idade" label="Idade" type="number" placeholder="Idade do Paciente" v-model="form.idade" class="pt-4" />
                <div class="flex w-full gap-4 pt-4">
                    <InputComponent required id="pressaosistolica" label="PA Sistólica" type="number" placeholder="Pressão Sistólica" v-model="form.pressaoSistolica" />
                    <InputComponent required id="pressaodiastolica" label="PA Diastólica" type="number" placeholder="Pressão Diastólica" v-model="form.pressaoDiastolica" />
                </div>
                <InputComponent required id="fc" label="Frequência Cardíaca (BPM)" type="number" placeholder="Frequência Cardíaca" v-model="form.fc" class="pt-4" />
                <InputComponent required id="fr" label="Frequência Respiratória (MPM)" type="number" placeholder="Frequência Respiratória" v-model="form.fr" class="pt-4" />
                <InputComponent required id="temp" label="Temperatura Corporal (ºC)" type="number" placeholder="Temperatura Corporal" v-model="form.temp" class="pt-4" />
                <InputComponent required id="oxigenacao" label="Oxigenação (%)" type="number" placeholder="Oxigenação" v-model="form.oxigenacao" class="pt-4" />
                <InputComponent required id="dextro" label="Dextro (mg/dl)" type="number" placeholder="Dextro" v-model="form.dextro" class="pt-4" />
                <div class="flex w-full gap-4 pt-4">
                    <InputComponent required id="altura" label="Altura (cm)" type="number" placeholder="Altura" v-model="form.altura" />
                    <InputComponent required id="peso" label="Peso (kg)" type="number" placeholder="Peso" v-model="form.peso" />
                </div>
                <div class="flex gap-4 pt-4 items-center justify-end w-full">
                    <InputComponent required id="glasgow" label="Glasgow" type="number" placeholder="Glasgow" v-model="form.glasgow" />
                    <NuxtLink target="_blank" class="question-mark" to="https://cafecirurgico.org/wp-content/uploads/2023/01/Escala-de-Coma-de-Glasgow-768x960.jpg"></NuxtLink>
                </div>
                <SelectComponent id="deambula" label="Deambula" :options="deambulaOptions" v-model="form.deambula" class="pt-4" />
                <InputComponent required id="diurese" label="Diurese" type="number" placeholder="Diurese" v-model="form.diurese" class="pt-4" />
                <InputComponent required id="evacuacao" label="Evacuação" type="number" placeholder="Evacuação" v-model="form.evacuacao" class="pt-4" />
                <InputComponent required id="alimentacao" label="Alimentação" type="text" placeholder="Alimentação" v-model="form.alimentacao" class="pt-4" />
                <TextAreaComponent required id="admissao" label="Admissão" placeholder="Admissão do Paciente" v-model="form.admissao" class="pt-4" />
                <TextAreaComponent required id="evolucao" label="Evolução de Enfermagem" placeholder="Evolução de Enfermagem" v-model="form.evolucao" class="pt-4" />
                <button type="submit" class="mt-6 bg-blue-500 text-white py-2 px-4 rounded-md">Salvar Paciente</button>
            </form>
        </div>
    </div>
</template>

<script setup lang="ts">


const router = useRouter()

// Estado dos campos do formulário
const form = ref({
    nome: '',
    idade: '',
    pressaoSistolica: '',
    pressaoDiastolica: '',
    fc: '',
    fr: '',
    temp: '',
    oxigenacao: '',
    dextro: '',
    altura: '',
    peso: '',
    glasgow: '',
    deambula: '',
    diurese: '',
    evacuacao: '',
    alimentacao: '',
    admissao: '',
    evolucao: ''
});

const deambulaOptions = ref([
    { value: 'sim', label: 'Sim' },
    { value: 'nao', label: 'Não' },
    { value: 'aux', label: 'Com Auxílio' },
]);

// Função para gerar um ID aleatório
function generateRandomId() {
    return 'id-' + Math.random().toString(36).substr(2, 9);
}

// Função para salvar os dados no localStorage
function saveToLocalStorage(newPaciente: any) {
    const existingData = JSON.parse(localStorage.getItem('pacientes') || '[]');
    existingData.push(newPaciente);
    localStorage.setItem('pacientes', JSON.stringify(existingData));
}

// Função para restaurar os dados do localStorage
function loadFromLocalStorage() {
    const savedData = localStorage.getItem('pacientes');
    if (savedData) {
        // Aqui você pode adicionar lógica para mostrar os pacientes na UI, se necessário.
    }
}

// Manipulador de envio do formulário
function handleSubmit() {
    // Crie um objeto de paciente com os dados do formulário e adicione um ID aleatório
    const paciente = {
        id: generateRandomId(),
        nome: form.value.nome,
        idade: form.value.idade,
        pressaoSistolica: form.value.pressaoSistolica,
        pressaoDiastolica: form.value.pressaoDiastolica,
        fc: form.value.fc,
        fr: form.value.fr,
        temp: form.value.temp,
        oxigenacao: form.value.oxigenacao,
        dextro: form.value.dextro,
        altura: form.value.altura,
        peso: form.value.peso,
        glasgow: form.value.glasgow,
        deambula: form.value.deambula,
        diurese: form.value.diurese,
        evacuacao: form.value.evacuacao,
        alimentacao: form.value.alimentacao,
        admissao: form.value.admissao,
        evolucao: form.value.evolucao
    };

    // Salve o paciente no localStorage
    saveToLocalStorage(paciente);

    router.push('/')
}

// Carregue os dados do localStorage ao montar o componente
onMounted(loadFromLocalStorage);
</script>

<style>
.question-mark {
    background-image: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iODAwIiBoZWlnaHQ9IjgwMCIgdmlld0JveD0iMCAwIDgwMCA4MDAiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxnIGNsaXAtcGF0aD0idXJsKCNjbGlwMF8zMjNfMikiPgo8cGF0aCBkPSJNMzk5Ljk5OSA4MDBDMTc5LjQ0MSA4MDAgMCA2MjAuNTc1IDAgMzk5Ljk5OUMwIDE3OS40MjMgMTc5LjQ0MSAwIDM5OS45OTkgMEM2MjAuNTU2IDAgNzk5Ljk5NyAxNzkuNDQxIDc5OS45OTcgMzk5Ljk5OUM3OTkuOTk3IDYyMC41NTYgNjIwLjU3NSA4MDAgMzk5Ljk5OSA4MDBaTTM5OS45OTkgNjQuNDcxN0MyMTQuOTg2IDY0LjQ3MTcgNjQuNDcxNyAyMTQuOTg2IDY0LjQ3MTcgMzk5Ljk5OUM2NC40NzE3IDU4NS4wMTIgMjE0Ljk4NiA3MzUuNTI2IDM5OS45OTkgNzM1LjUyNkM1ODUuMDEyIDczNS41MjYgNzM1LjUyNiA1ODUuMDEyIDczNS41MjYgMzk5Ljk5OUM3MzUuNTI2IDIxNC45ODYgNTg1LjAyNyA2NC40NzE3IDM5OS45OTkgNjQuNDcxN1oiIGZpbGw9IiM2QjcyODAiLz4KPHBhdGggZD0iTTMwNy44NTEgMzExLjkwMkMzMTIuNTkxIDI5OS43MzcgMzE5LjE5OCAyODkuMjI1IDMyNy42ODUgMjgwLjMxOEMzMzYuMiAyNzEuMzY5IDM0Ni40NjkgMjY0LjQzMyAzNTguNDkyIDI1OS40NjNDMzcwLjQ5OCAyNTQuNDM2IDM4My45MjggMjUxLjk1MSAzOTguNzkyIDI1MS45NTFDNDE3Ljk2NSAyNTEuOTUxIDQzMy45NjQgMjU0LjU3OCA0NDYuODA1IDI1OS44NjVDNDU5LjYzIDI2NS4xMzUgNDY5Ljk1NyAyNzEuNyA0NzcuOCAyNzkuNTEzQzQ4NS42MjcgMjg3LjM1NSA0OTEuMjQzIDI5NS44IDQ5NC42MTggMzA0LjgyQzQ5Ny45NzkgMzEzLjg4MiA0OTkuNjc0IDMyMi4zNDMgNDk5LjY3NCAzMzAuMTU2QzQ5OS42NzQgMzQzLjA5NyA0OTcuOTc5IDM1My43ODEgNDk0LjYxOCAzNjIuMTU0QzQ5MS4yNDMgMzcwLjUyNyA0ODcuMDUgMzc3LjY4MSA0ODIuMDUxIDM4My42MjVDNDc3LjAzOSAzODkuNTcxIDQ3MS41MjMgMzk0LjY0MSA0NjUuNDM0IDM5OC44MjFDNDU5LjM3NCA0MDMuMDE0IDQ1My42MjggNDA3LjE5NCA0NDguMjI4IDQxMS4zODdDNDQyLjgyOCA0MTUuNTY3IDQzOC4wMzEgNDIwLjM0OSA0MzMuODUxIDQyNS43NDlDNDI5LjY1NyA0MzEuMTM2IDQyNy4wMTQgNDM3Ljg5OSA0MjUuOTUzIDQ0NS45ODdWNDYxLjM4NEgzNzEuMjYyVjQ0My4xNDNDMzcyLjA2NyA0MzEuNTM3IDM3NC4zMDYgNDIxLjgyOCAzNzcuOTQgNDE0LjAwMkMzODEuNTg5IDQwNi4xNzUgMzg1LjgzNyAzOTkuNDgxIDM5MC42OTMgMzkzLjkzOUMzOTUuNTYzIDM4OC40MjMgNDAwLjY5MSAzODMuNjExIDQwNi4xMDQgMzc5LjU2MUM0MTEuNDkgMzc1LjQ5NyA0MTYuNDczIDM3MS40NDYgNDIxLjA4MyAzNjcuNDM4QzQyNS42NTIgMzYzLjM1OCA0MjkuMzg1IDM1OC45MjIgNDMyLjIyOSAzNTQuMDUzQzQzNS4wNTcgMzQ5LjIxMyA0MzYuMzM4IDM0My4wOTUgNDM2LjA2MyAzMzUuODEyQzQzNi4wNjMgMzIzLjM4OCA0MzMuMDMyIDMxNC4yMTIgNDI2Ljk0MyAzMDguMjc5QzQyMC44ODMgMzAyLjMxOSA0MTIuNDM4IDI5OS4zNTkgNDAxLjYyMyAyOTkuMzU5QzM5NC4zNCAyOTkuMzU5IDM4OC4wNjYgMzAwLjc2NyAzODIuNzkzIDMwMy41OTdDMzc3LjUyIDMwNi40MjggMzczLjIxMyAzMTAuMjMzIDM2OS44MjUgMzE0Ljk1N0MzNjYuNDUgMzE5LjY5NyAzNjMuOTUgMzI1LjIzOSAzNjIuMzQyIDMzMS41NjFDMzYwLjcxOCAzMzcuOTM4IDM1OS45MTUgMzQ0LjcxNiAzNTkuOTE1IDM1Mi4wNDFIMzAwLjM3MUMzMDAuNjI3IDMzNy40MjMgMzAzLjExMiAzMjQuMDggMzA3Ljg1MSAzMTEuOTAyWk00MjkuMTg1IDQ4NS42OThWNTQ4LjA1N0gzNjUuNTc0VjQ4NS42OThINDI5LjE4NVoiIGZpbGw9IiM2QjcyODAiLz4KPC9nPgo8ZGVmcz4KPGNsaXBQYXRoIGlkPSJjbGlwMF8zMjNfMiI+CjxyZWN0IHdpZHRoPSI4MDAiIGhlaWdodD0iODAwIiBmaWxsPSJ3aGl0ZSIvPgo8L2NsaXBQYXRoPgo8L2RlZnM+Cjwvc3ZnPgo=);
    background-repeat: no-repeat;
    background-position: right;
    width: 24px;
    height: 24px;
    background-size: 100%;
    display: inline-block;
    position: relative;
    top: 14px;
}

.go-back {
    background-repeat: no-repeat;
    background-position: right;
    width: 24px;
    height: 24px;
    background-size: 100%;
    display: inline-block;
    position: absolute;
    transform: translateY(-50%);
    top: 55%;
    background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz48IS0tIFVwbG9hZGVkIHRvOiBTVkcgUmVwbywgd3d3LnN2Z3JlcG8uY29tLCBHZW5lcmF0b3I6IFNWRyBSZXBvIE1peGVyIFRvb2xzIC0tPgo8c3ZnIHdpZHRoPSI4MDBweCIgaGVpZ2h0PSI4MDBweCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgo8cGF0aCBkPSJNMjAuMzI4NyAxMS4wMDAyVjEzLjAwMDJMNy41MDA0MiAxMy4wMDAyTDEwLjc0MjkgMTYuMjQyOEw5LjMyODczIDE3LjY1N0wzLjY3MTg4IDEyLjAwMDFMOS4zMjg3MyA2LjM0MzI2TDEwLjc0MjkgNy43NTc0N0w3LjUwMDE5IDExLjAwMDJMMjAuMzI4NyAxMS4wMDAyWiIgZmlsbD0iIzAwMDAwMCIvPgo8L3N2Zz4=);
}
</style>
