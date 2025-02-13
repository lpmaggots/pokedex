<template>
  <Navbar />

  <main>
    <router-view></router-view>
  </main>

  <Footer />
</template>

<script setup>
  import Navbar from './components/shared/Navbar.vue'
  import Footer from './components/shared/Footer.vue'
</script>