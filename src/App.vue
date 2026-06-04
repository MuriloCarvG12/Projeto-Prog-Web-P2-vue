<script setup>
  import Header from "./components/Header.vue";
  import Dashboard from "./components/Dashboard.vue";
  import Reserva from "./components/Reserva.vue";
  import SobreNos from "./components/SobreNos.vue";

  import {ref, computed, onMounted } from "vue"

  const wagons = ref([]);

    async function fetchWagons() {
    const url = "http://localhost:8080/GetCarriages?CarriageType=PassengerCarriage";
    try {
        const response = await fetch(url);
        if (!response.ok) throw new Error(`Response status: ${response.status}`);
        wagons.value = await response.json();
    } catch (error) {
        console.error(error.message);
    }
    }

    onMounted(() => {
    fetchWagons(); 
    });

  const CurrentPageState = ref(1)
  const currentComponent = computed(() => {
    switch (CurrentPageState.value) {
        case 1:
            return Dashboard;
        case 2:
            return Reserva;
        case 3:
            return SobreNos;
        default:
            return null;
    }
});

async function receiveEmit() {
    await fetchWagons();
}

</script>

<template id="app">
  <Header/>
  <div style=" display: flex; flex-direction: row; height:100%; width:100%">
    <div class="side-bar">
        <div class="menu-button" @click="CurrentPageState = 1">
            DashBoard - Trens
        </div>
        <div class="menu-button" @click="CurrentPageState = 2">
            Reserva 
        </div>
        <div class="menu-button" @click="CurrentPageState = 3">
            Sobre Nós
        </div>
    </div>
    <div style="display: flex; flex-direction: column; background-color:red; height:100%; width:100%">
        <component :is="currentComponent" :wagons="wagons" @seatReserved="receiveEmit"/>

    </div>
  </div>
</template>

<style>
</style>