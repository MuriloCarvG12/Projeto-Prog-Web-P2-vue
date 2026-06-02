<script setup>

    const props = defineProps({
        wagons: Array
    });

    
</script>

<template>
    <div class="page">
        <h1>Dashboard - Trens</h1>

        <div class="grid-container">
            <div v-for="wagon in wagons" :key="wagon.Id" class="wagon-card">
            
                <h2>Vagão - {{ wagon.Id }}</h2>

                <div class="seats-grid">
                <div 
                    v-for="seat in wagon.CarriageSeats" 
                    :key="seat.Id"
                    :class="seat.SeatTaken ? 'seat-taken' : 'seat-free'"
                >
                    <p>{{ seat.SeatNumber }}</p>
                </div>
            </div>

        </div>
    </div>
        
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
    overflow-y: scroll;
    align-items: center;
}

.grid-container
{
    background-color: azure;
    border-style: solid;
    border-width: 2px;
    border-color: #d8dbe2;
    border-radius: 2%;
    width: 80%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.wagon-card
{
    width: 60%;
    height: 80%;
    background-color: white;
    border-style: solid;
    border-width: 2px;
    border-color: #535353;
    border-radius: 2%;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 5%;
}

.seats-grid {
  display: grid;
  grid-template-columns: repeat(5, 100px); /* 4 seats per row */
  gap: 10px;
  padding: 10px;
}

input {
    padding: 8px;
}

button {
    padding: 10px;
}

.seat-free {
  width: 50px;
  height: 50px;
  background-color: greenyellow;
  border-radius: 8px;
  
}

.seat-free:hover
{
    cursor: pointer;
}

.seat-taken {
  width: 50px;
  height: 50px;
  background-color: indianred;
  border-radius: 8px;
}
</style>