<template>
  <div id="app">
    <Navbar />
    <div class="page-container" ref="scrollContainer">
      <div class="section" id="homeSection"><HomeSection /></div>
      <div class="section scrollable" id="aboutSection"><AboutSection /></div>
      <div class="section" id="contactSection"><ContactSection /></div>
    </div>
    <Footer />
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
import { useHead } from '@vueuse/head';
import Navbar from './components/Navbar.vue';
import HomeSection from './components/HomeSection.vue';
import ContactSection from './components/ContactSection.vue';
import AboutSection from './components/AboutSection.vue';
import Footer from './components/Footer.vue';
import './assets/styles/fonts.css';

export default {
  name: 'App',
  components: {
    Navbar,
    HomeSection,
    ContactSection,
    AboutSection,
    Footer,
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
useHead({
  title: 'Webgrind - Software Development & IT Solutions',
  meta: [
    {
      name: 'description',
      content:
        'Your one-stop shop for software development, mobile apps, and IT infrastructure services.',
    },
    {
      property: 'og:title',
      content: 'Webgrind - Software Development & IT Solutions',
    },
    {
      property: 'og:description',
      content:
        'Your one-stop shop for software development, mobile apps, and IT infrastructure services.',
    },
    {
      property: 'og:image',
      content: 'https://webgrind.nl/img/webgrindlogonotext.d5e9d888.svg',
    }, // Replace with your logo image URL
    { property: 'og:url', content: 'https://www.webgrind.nl' },
  ],
  script: [
    {
      type: 'application/ld+json',
      innerHTML: JSON.stringify({
        '@context': 'http://schema.org',
        '@type': 'WebSite',
        name: 'Webgrind',
        url: 'https://www.webgrind.nl',
        potentialAction: {
          '@type': 'SearchAction',
          target: 'https://www.webgrind.nl/search?q={search_term_string}',
          'query-input': 'required name=search_term_string',
        },
      }),
    },
  ],
});
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

  overflow: hidden; /* Prevent free scrolling */
}

.page-container {
  height: 100vh; /* Full viewport height for each section */
  overflow-y: auto; /* Enable vertical scrolling */
  scroll-snap-type: y mandatory; /* Enable scroll-snap for vertical scrolling */
  scroll-behavior: smooth; /* Smooth scroll */
}

.section {
  height: 100vh; /* Each section takes full viewport height */
  scroll-snap-align: start; /* Align sections to the top of the viewport */
}

.section.scrollable {
  overflow-y: auto;
  max-height: 100vh; /* Allow scroll but limited */
  padding-bottom: 50px;
  padding-top: 50px;
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
