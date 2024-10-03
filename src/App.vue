<template>
  <div id="app">
    <Navbar />
    <HomeSection />
    <AboutSection />
    <ContactSection />
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import HomeSection from "./components/HomeSection.vue";
import ContactSection from "./components/ContactSection.vue";
import AboutSection from "./components/AboutSection.vue";

import './assets/styles/fonts.css';

export default {
  name: 'App',
  components: {
    Navbar, 
    HomeSection,
    ContactSection,
    AboutSection,
  },
};
</script>

<style>
/* Apply the global gradient background to the entire app */
html, body {
  height: 100%;
  margin: 0;
  padding: 0;
  background: linear-gradient(135deg, #162945, #0a0a0a); /* Gradient background */
  background-attachment: fixed; /* Keeps the background fixed when scrolling */
  background-size: cover; /* Ensures the background covers the whole screen */
  font-family: 'Webgrind', Arial, sans-serif; /* Apply custom font globally */
}

#app {
  min-height: 100vh; /* Ensures the content always fills the viewport height */
  position: relative;
}

</style>
