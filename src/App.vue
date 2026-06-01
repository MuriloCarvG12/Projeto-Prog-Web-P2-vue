<script setup>
  import Header from "./components/Header.vue";
  import Dashboard from "./components/Dashboard.vue";
  import Reports from "./components/Reports.vue";
  import Settings from "./components/Settings.vue";

  import {ref, computed } from "vue"


  const CurrentPageState = ref(1)
  const currentComponent = computed(() => {
    switch (CurrentPageState.value) {
        case 1:
            return Dashboard;
        case 2:
            return Reports;
        case 3:
            return Settings;
        default:
            return null;
    }
});

</script>

<template id="app">
  <Header/>
  <div style=" display: flex; flex-direction: row; height:100%; width:100%">
    <div class="side-bar">
        <div class="menu-button" @click="CurrentPageState = 1">
            Dashboard
        </div>
        <div class="menu-button" @click="CurrentPageState = 2">
            Reports
        </div>
        <div class="menu-button" @click="CurrentPageState = 3">
            Settings
        </div>
    </div>
    <div style="display: flex; flex-direction: column; background-color:red; height:100%; width:100%">
        <component :is="currentComponent" />
    </div>
  </div>
</template>

<style>
</style>