<script setup>
    import {ref, computed, onMounted } from "vue"

    const props = defineProps({
        wagons: Array
    });

    const currentWagonIndex = ref(0);

    const currentWagon = computed(() => props.wagons[currentWagonIndex.value]);

    const emit = defineEmits(['seatReserved']);

    function IncreaseIndex()
    {
        if(currentWagonIndex.value < props.wagons.length - 1)
        {
            currentWagonIndex.value++;
        }
    };

    function DecreaseIndex()
    {
        if(currentWagonIndex.value > 0)
        {
            currentWagonIndex.value--;
        }
    };

    async function ReserveSeat(SeatCode, CarriageCode, UserId)
    {
      try 
      {
        const url = "http://localhost:8080/ReserveCarriage/Seat";
        const response = await fetch 
              (url, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ seatCode: SeatCode, carriageCode: CarriageCode, userCode: UserId }),
                
              })
      
        if (!response.ok) throw new Error(`Response status: ${response.status}`);
        const updatedSeat = await response.json();
        emit('seatReserved', updatedSeat);
   
      } 
      catch (error)
      {
        console.error(error.message);
      }
        
    }
    
</script>

<template>
    <div class="page">

        <div class="dash-header">

            <span class="dash-label">
                <span class="orange-dot" aria-hidden="true"></span>
                Dashboard - Reservas Assentos
            </span>
            
            <div class="dash-rule"></div>
        
        </div>

        <div class="grid-container">
            <div style="display: flex; flex-direction: column; align-items: center;">

                <div class="nav-row">
                <div class="nav-btn" @click="DecreaseIndex()">
                    <i class="ti ti-chevron-left" aria-hidden="true"></i>
                </div>
                <span class="wagon-label">Vagão-{{ String(currentWagon.Id).padStart(3, '0') }}</span>
                <div class="nav-btn" @click="IncreaseIndex()">
                    <i class="ti ti-chevron-right" aria-hidden="true"></i>
                </div>
                </div>

                <div class="wagon-card">
                <div class="seats-grid">
                    <div
                    v-for="seat in currentWagon.CarriageSeats"
                    :key="seat.Id"
                    :class="seat.SeatTaken ? 'seat-taken' : 'seat-free'"
                    v-on:click="ReserveSeat(seat.seatNumber, currentWagon.Id, 1)"
                    >
                    <p>{{ seat.SeatNumber }}</p>
                    </div>
                </div>
                <div class="legend">
                    <div class="legend-item"><div class="legend-dot dot-taken"></div> ocupado</div>
                    <div class="legend-item"><div class="legend-dot dot-free"></div> disponível</div>
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
    background-color: rgb(255, 255, 255);
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
    width: auto;
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
  grid-template-columns: repeat(5, 100px);
  gap: 10px;
  padding: 10px;
  justify-content: center;
  align-items: center;
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

.dash-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 2rem;
}

.dash-label {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #888;
  white-space: nowrap;
}

.orange-dot {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #E06000;
  margin-right: 6px;
  vertical-align: middle;
}

.dash-rule {
  flex: 1;
  height: 0.5px;
  background: #e5e5e5;
  width: 100%;
}

/* Panel */
.panel {
  background: #ffffff;
  border: 0.5px solid #e0e0e0;
  border-radius: 12px;
  overflow: hidden;
}

.panel-head {
  padding: 1.5rem 1.5rem 1rem;
  border-bottom: 0.5px solid #e0e0e0;
}

.panel-name {
  font-size: 22px;
  font-weight: 500;
  margin: 0 0 4px;
  letter-spacing: -0.3px;
}

.panel-sub {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #888;
  margin: 0;
}

.dash-carriage 
{
  font-family: 'DM Mono', monospace;
  font-size: 25px;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #6e6e6e;
  white-space: nowrap;   
  text-align: center;
}

.w-id {
  font-family: 'DM Mono', monospace;
  font-size: 20px;
  font-weight: 500;
  background: #FFF3EA;
  color: #C45000;
  border: 0.5px solid #FFCFAB;
  border-radius: 6px;
  padding: 4px 8px;
  text-align: center;
  letter-spacing: 0.04em;
}

.arrow-left {
  width: 0;
  height: 0;
  border-top: 30px solid transparent;
  border-bottom: 30px solid transparent;
  border-right: 48px solid #E06000;
}

.arrow-right {
  width: 0;
  height: 0;
  border-top: 30px solid transparent;
  border-bottom: 30px solid transparent;
  border-left: 48px solid #E06000;
}

.arrow-left:hover {
  width: 0;
  height: 0;
  border-top: 30px solid transparent;
  border-bottom: 30px solid transparent;
  border-right: 48px solid #bd5303;
  cursor: pointer;
}

.arrow-right:hover {
  width: 0;
  height: 0;
  border-top: 30px solid transparent;
  border-bottom: 30px solid transparent;
  border-left: 48px solid #bd5303;
  cursor: pointer;
}

.nav-row {
  display: flex;
  align-items: center;
  gap: 24px;
  margin-bottom: 1.25rem;
}

.nav-btn {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  border: 0.5px solid #d0d0d0;
  background: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: #888;
  font-size: 16px;
  transition: background 0.12s;
}

.nav-btn:hover { background: #f5f5f5; }

.wagon-label {
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.08em;
  background: #FFF3EA;
  color: #C45000;
  border: 0.5px solid #FFCFAB;
  border-radius: 6px;
  padding: 4px 12px;
}

.wagon-card {
  background: #ffffff;
  border: 0.5px solid #e0e0e0;
  border-radius: 12px;
  padding: 1.5rem;
  width: 100%;
  max-width: 480px;
}

.seats-grid {
  display: grid;
  width: 100%;
  grid-template-columns: repeat(4, 80px);
  gap: 8px;
}

.seat-free, .seat-taken {
  width: 80px;
  height: 80px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  font-weight: 500;
}

.seat-free {
  background: #f5f5f5;
  border: 0.5px solid #e0e0e0;
  color: #888;
}

.seat-taken {
  background: #FFF3EA;
  border: 0.5px solid #FFCFAB;
  color: #C45000;
}

.seat-free p, .seat-taken p { margin: 0; }

.legend {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-top: 1rem;
  justify-content: flex-end;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 12px;
  color: #888;
}

.legend-dot {
  width: 10px;
  height: 10px;
  border-radius: 3px;
}

.dot-taken { background: #FFF3EA; border: 0.5px solid #fcb599; }
.dot-free  { background: #f5f5f5; border: 0.5px solid #e0e0e0; }

</style>