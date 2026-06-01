<script setup>
const trens = [
    { id: 1, nome: "Expresso Norte", vagas: 45 },
    { id: 2, nome: "Expresso Sul", vagas: 12 },
    { id: 3, nome: "Regional", vagas: 28 }
];
</script>

<template>
    <div class="page">
        <h1>Dashboard - Trens</h1>

        <div
            v-for="trem in trens"
            :key="trem.id"
            class="card"
        >
            <h3>{{ trem.nome }}</h3>
            <p>Vagas disponíveis: {{ trem.vagas }}</p>
        </div>
    </div>
</template>

<style scoped>
.page {
    padding: 20px;
    background-color: white;
    height: 100%;
}

.card {
    padding: 15px;
    margin-top: 10px;
    border: 1px solid #ddd;
    border-radius: 8px;
}
</style>