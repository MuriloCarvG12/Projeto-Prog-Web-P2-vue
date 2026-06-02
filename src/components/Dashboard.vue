<script setup>

    const props = defineProps({
        wagons: Array
    });


    
</script>

<template>
    <div class="page">
        <h1>Dashboard - Trens</h1>

        <div
            v-for="wagon in wagons"
            :key="wagon.Id"
            class="card"
        >
            <h3>{{ wagon.RouteCode }}</h3>
            <h3>{{ wagon.CarriageClass }}</h3>
              <p>{{ wagon.CarriageSeats.filter(seat => !seat.SeatTaken).length }} seats available</p>
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