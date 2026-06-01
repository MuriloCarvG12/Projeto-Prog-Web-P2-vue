<script setup>
import { ref } from "vue";

const nome = ref("");
const assento = ref("");

function reservar() {
    alert(
        `Reserva realizada!\nPassageiro: ${nome.value}\nAssento: ${assento.value}`
    );
}
</script>

<template>
    <div class="page">
        <h1>Reserva</h1>

        <input
            v-model="nome"
            placeholder="Nome do passageiro"
        />

        <input
            v-model="assento"
            placeholder="Número do assento"
        />

        <button @click="reservar">
            Reservar
        </button>
    </div>
</template>

<style scoped>
.page {
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 10px;
    background-color: white;
    height: 100%;
}

input {
    padding: 8px;
}

button {
    padding: 10px;
}
</style>