<template>
  <v-app>
    <div class="background-effects">
      <div class="particles"></div>
      <div class="gradient-overlay"></div>
    </div>
    <!-- Mobile Header -->
    <v-app-bar
      v-if="$vuetify.display.smAndDown"
      color="primary"
      density="compact"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Greenhouse Monitor</v-toolbar-title>
    </v-app-bar>

    <!-- Navigation Drawer -->
      <v-navigation-drawer 
      v-if="!$route.path.includes('dashboard')" 
      v-model="drawer" 
      permanent 
      class="nav-drawer"
    >
      <NavBar />
    </v-navigation-drawer>

    <!-- Main Content -->
    <v-main class="main-content">
      <v-container fluid>
      <router-view></router-view>
    </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import NavBar from './components/NavBar.vue'

const drawer = ref(true)

onMounted(() => {
  const particles = document.querySelector('.particles')
  for (let i = 0; i < 50; i++) {
    const particle = document.createElement('div')
    particle.classList.add('particle')
    particles.appendChild(particle)
  }
})
</script>

<style>
/* Transitions */
.page-enter-active, .page-leave-active {
  transition: all 0.4s ease;
}

.page-enter-from, .page-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.slide-enter-active, .slide-leave-active {
  transition: all 0.4s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(50px);
}

.slide-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}

/* Root Variables */
:root {
  --gradient-primary: linear-gradient(135deg, #283048 0%, #859398 100%);
  --gradient-secondary: linear-gradient(120deg, #24243e 0%, #302b63 100%);
  --accent: #6C63FF;
  --success: #00F260;
  --warning: #FFA63D;
  --card-bg: rgba(255, 255, 255, 0.9);
}

/* Layout Components */
.nav-drawer {
  background: rgba(255, 255, 255, 0.1) !important;
  backdrop-filter: blur(10px);
  border-right: 1px solid rgba(255, 255, 255, 0.1);
}

.main-content {
  position: relative;
  z-index: 1;
  background: transparent !important;
}

/* Cards and UI Elements */
.glass-card {
  background: rgba(255, 255, 255, 0.25) !important;
  backdrop-filter: blur(15px) !important;
  border: 1px solid rgba(255, 255, 255, 0.3) !important;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.15) !important;
}

.metric-card {
  background: rgba(255, 255, 255, 0.15) !important;
  backdrop-filter: blur(12px);
}

.metric-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
  border-color: rgba(255, 255, 255, 0.3);
}

/* Buttons */
.v-btn {
  background-color: #f48fb1 !important;
  color: white !important;
  transition: all 0.3s ease !important;
}

.v-btn:hover {
  background-color: #f8bbd0 !important;
  transform: translateY(-2px);
}

/* Background Effects */
.v-application {
  background: var(--gradient-primary) !important;
  min-height: 100vh;
  position: relative;
  overflow: hidden;
}

.v-application::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 20%, rgba(255, 255, 255, 0.1) 0%, transparent 40%),
    radial-gradient(circle at 80% 80%, rgba(255, 255, 255, 0.1) 0%, transparent 40%);
  z-index: 0;
}

.background-effects {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  overflow: hidden;
}

.gradient-overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(to right, #141e30, #243b55);
  opacity: 0.8;
}

.particles {
  position: absolute;
  width: 100%;
  height: 100%;
}

.particle {
  position: absolute;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  width: 4px;
  height: 4px;
  animation: float 20s infinite linear;
}

@keyframes float {
  0% {
    transform: translateY(0) translateX(0);
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: translateY(-100vh) translateX(100vw);
    opacity: 0;
  }
}

.dashboard-container {
  backdrop-filter: blur(10px);
  background: var(--glass-effect);
  border-radius: 24px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}
</style>