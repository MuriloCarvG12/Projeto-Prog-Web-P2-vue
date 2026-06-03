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

    <div class="dash-header">
      <span class="dash-label">
        <span class="orange-dot" aria-hidden="true"></span>
        Dashboard — Trens
      </span>
      <div class="dash-rule"></div>
    </div>

    <div class="panel">
      <div class="panel-head">
        <p class="panel-name">Carruagens</p>
        <p class="panel-sub">Lista de vagões disponíveis</p>
      </div>

      <div class="wagon-list">
        <div
          v-for="wagon in wagons"
          :key="wagon.Id"
          class="wagon-card"
        >
          <span class="w-id">V-{{ String(wagon.Id).padStart(3, '0') }}</span>

          <div class="w-main">
            <span class="w-route">Rota {{ wagon.RouteCode }}</span>
            <span class="w-class">{{ wagon.CarriageClass }}</span>
          </div>

          <span class="w-seats">
            <strong>{{ wagon.CarriageSeats.filter(s => !s.SeatTaken).length }}</strong> assentos
          </span>

          <span :class="['badge', isWagonFull(wagon) ? 'badge-full' : 'badge-ok']">
            {{ isWagonFull(wagon) ? 'ocupado' : 'disponível' }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500&family=DM+Mono:wght@400;500&display=swap');

.page {
  font-family: 'DM Sans', sans-serif;
  padding: 2rem;
  background-color: #ffffff;
  min-height: 100%;
  color: #1a1a1a;
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
}

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

.wagon-list {
  padding: 0.75rem 1rem;
}

.wagon-card {
  display: grid;
  grid-template-columns: 56px 1fr auto auto;
  align-items: center;
  gap: 16px;
  padding: 0.875rem 0.75rem;
  border-radius: 8px;
  transition: background 0.15s;
  cursor: default;
}

.wagon-card:hover {
  background: #f8f8f8;
}

.wagon-card + .wagon-card {
  border-top: 0.5px solid #e5e5e5;
  border-radius: 0;
}

.wagon-card:hover {
  border-radius: 8px;
}

.wagon-card:hover + .wagon-card {
  border-color: transparent;
}

.w-id {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  font-weight: 500;
  background: #FFF3EA;
  color: #C45000;
  border: 0.5px solid #FFCFAB;
  border-radius: 6px;
  padding: 4px 8px;
  text-align: center;
  letter-spacing: 0.04em;
}

.w-main {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.w-route {
  font-size: 14px;
  font-weight: 500;
}

.w-class {
  font-size: 12px;
  color: #888;
}

.w-seats {
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  color: #888;
  text-align: right;
  white-space: nowrap;
}

.w-seats strong {
  font-weight: 500;
  color: #1a1a1a;
}

.badge {
  font-size: 11px;
  font-weight: 500;
  padding: 3px 10px;
  border-radius: 999px;
  white-space: nowrap;
}

.badge-ok {
  background: #EAF3DE;
  color: #3B6D11;
  border: 0.5px solid #97C459;
}

.badge-full {
  background: #FCEBEB;
  color: #791F1F;
  border: 0.5px solid #F09595;
}
</style>