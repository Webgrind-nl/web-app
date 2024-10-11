<template>
  <div id="app">
    <Navbar />
    <HomeSection />
    <AboutSection />
    <ContactSection />
    <button
      v-show="showScrollTopButton"
      @click="scrollToTop"
      class="scroll-to-top"
      aria-label="Scroll to top"
    >
      ⬆️
    </button>
  </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import Navbar from './components/Navbar.vue';
import HomeSection from './components/HomeSection.vue';
import ContactSection from './components/ContactSection.vue';
import AboutSection from './components/AboutSection.vue';
import './assets/styles/fonts.css';

export default {
  name: 'App',
  components: {
    Navbar,
    HomeSection,
    ContactSection,
    AboutSection,
  },
  setup() {
    // Correctly define reactive variables and lifecycle hooks within setup()
    const showScrollTopButton = ref(false);

    // Smooth Scroll to Top Function
    const scrollToTop = () => {
      window.scrollTo({
        top: 0,
        behavior: 'smooth',
      });
    };

    // Watch Scroll Position and Show Button
    const handleScroll = () => {
      showScrollTopButton.value = window.scrollY > 200; // Show button if scrolled more than 200px
    };

    // Add event listener for scroll on component mount
    onMounted(() => {
      window.addEventListener('scroll', handleScroll);
    });

    // Remove event listener when component is destroyed
    onBeforeUnmount(() => {
      window.removeEventListener('scroll', handleScroll);
    });

    // Return the variables and methods to the template
    return { showScrollTopButton, scrollToTop };
  },
};
</script>

<style>
/* Apply the global gradient background to the entire app */
html,
body {
  height: 100%;
  margin: 0;
  padding: 0;
  background: linear-gradient(
    135deg,
    #162945,
    #0a0a0a
  ); /* Gradient background */
  background-attachment: fixed; /* Keeps the background fixed when scrolling */
  background-size: cover; /* Ensures the background covers the whole screen */
  font-family: 'Webgrind', Arial, sans-serif; /* Apply custom font globally */
}

#app {
  min-height: 100vh; /* Ensures the content always fills the viewport height */
  position: relative;
}

/* Scroll to Top Button */
.scroll-to-top {
  position: fixed;
  bottom: 30px;
  right: 30px;
  background: linear-gradient(135deg, #6a0dad, #d16ba5, #45aaf2);
  color: white;
  border: none;
  border-radius: 50px;
  padding: 15px;
  font-size: 18px;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease, box-shadow 0.3s ease, opacity 0.3s ease;
  z-index: 1000;
  opacity: 0.8;
}

/* Hover Effect for Scroll Button */
.scroll-to-top:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.5);
  opacity: 1;
}
</style>
