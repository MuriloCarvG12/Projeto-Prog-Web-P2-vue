<script setup>

    const props = defineProps({
        wagons: Array
    });

    function isWagonFull(wagon) {
    return wagon.CarriageSeats.filter(seat => seat.SeatTaken).length === wagon.CarriageSeats.length;
    }
    
</script>

<template>
    <div class="page">
        <h1>Dashboard - Trens</h1>
        <div class="carriagesContainer">
             <p class = "ticket-logo"> Carruagens </p>
             <p class = "ticket-sub"> Lista de vagões disponíveis </p>
             <hr/>
            <div
            v-for="wagon in wagons"
            :key="wagon.Id"
            class="card"
             >
            <div style="display: flex; flex-direction: row; gap: 5%; justify-content: center;">
              <h3>Cód. Vagão - {{ wagon.Id }}</h3>  
              <div style="display: flex; flex-direction: column;">
                <h3>Cód. Rota - {{ wagon.RouteCode }}</h3>
                <h3>{{ wagon.CarriageClass }}</h3>
              </div>
              <p>{{ wagon.CarriageSeats.filter(seat => !seat.SeatTaken).length }} seats available</p>
              <div :class="isWagonFull(wagon) ? 'wagon-full' : 'wagon-available'">{{ isWagonFull(wagon) ? 'vagão ocupado' : 'vagão disponível' }}</div>
            </div>
        </div>
        </div>
        
    </div>
</template>

<style scoped>

.carriagesContainer
{
    display: flex;
    flex-direction: column;
    width: 80%;
    height: 100%;
    border-style: solid;
    border-width: 2px;
    border-color: #7a7a7a;
    border-radius: 2%;
}

.ticket-logo {
  font-family: 'Playfair Display', serif;
  font-size: 30px;
  font-weight: 500;
  letter-spacing: -0.3px;
  margin: 0 0 4px;
  text-align: center;
}

.ticket-sub {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 20px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  margin: 0;
  text-align: center;
}

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


.wagon-available {
  width: 10%;
  background: #EAF3DE;
  color: #27500A;
  border: 0.5px solid #97C459;
  text-align: center;
}

.wagon-full {
  width: 10%;
  background: #FCEBEB;
  color: #791F1F;
  border: 0.5px solid #F09595;
  text-align: center;
}
</style>