<template>
  <div class="min-h-screen bg-gray-100">
    <NavBar @toggle-sidebar="toggleSidebar" />
    <SideBar :isOpen="isSidebarOpen" @close-sidebar="closeSidebar" />
    <div :class="isSidebarOpen ? 'ml-64' : 'ml-0'" class="p-6 transition-all duration-300">
      <h1 class="text-2xl font-bold mb-6">Accueil</h1>
      <VideoGrid :videos="videos" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import NavBar from '../components/NavBar.vue';
import SideBar from '../components/SideBar.vue';
import VideoGrid from '../components/VideoGrid.vue';

const videos = ref([]);
const isSidebarOpen = ref(false);

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value;
};

const closeSidebar = () => {
  isSidebarOpen.value = false;
};

onMounted(async () => {
  try { 
    const response = await axios.get(`http://localhost:3000/video/`);
    video.value = response.data; 
  } catch (error) {
    console.error('Erreur lors de la récupération de la vidéo:', error);
  }
});

</script>