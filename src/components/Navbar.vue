<template>
  <nav class="navbar">
    <div class="navbar-container">
      <a href="#" class="logo">
        <img
          src="../assets/webgrindlogonotext.svg"
          class="logo-img"
          alt="Webgrind Logo"
        />
        <img
          src="../assets/webgrindtextonly.svg"
          class="logo-text"
          alt="Webgrind Text Logo"
        />
      </a>
      <button
        class="burger"
        @click="toggleMenu"
        aria-controls="navbar-content"
        aria-expanded="menuOpen"
      >
        <span class="burger-line"></span>
        <span class="burger-line"></span>
        <span class="burger-line"></span>
      </button>
      <div
        :class="{ 'nav-links': true, 'nav-active': menuOpen }"
        id="navbar-content"
      >
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">About Us</a></li>
          <li><a href="#">Services</a></li>
          <li><a href="#">Portfolio</a></li>
          <li><a href="#">FAQ</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue';

const menuOpen = ref(false);

function toggleMenu() {
  menuOpen.value = !menuOpen.value;
}
</script>

<style scoped>
/* Apply the same gradient as the page */
body,

/* Navbar Styling */
.navbar {
  width: 100%;
  position: sticky; /* Make it sticky */
  top: 0;
  left: 0;
  background: linear-gradient(135deg, #162945, #0a0a0a);
  z-index: 1000;
  background-attachment: fixed; /* Ensure the gradient stays fixed */
  padding: 10px 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  transition: background 0.3s ease-in-out, transform 0.3s ease;
}

/* Navbar Container */
.navbar-container {
  max-width: 1200px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  margin: auto;
}

/* Logo Styling */
.logo {
  display: flex;
  align-items: center;
}

.logo-img {
  height: 35px;
}

.logo-text {
  padding-left: 10px;
  height: 18px;
}

/* Navbar Links */
.nav-links {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  height: 100%;
  transition: transform 0.3s ease-in-out, opacity 0.3s ease;
}

.nav-links ul {
  display: flex;
  list-style: none;
  gap: 20px;
}

.nav-links ul li {
  padding: 10px;
}

.nav-links ul li a {
  color: #ffffff;
  text-decoration: none;
  font-weight: 500;
  position: relative;
  transition: color 0.3s ease-in-out;
}

/* Hover Effect for Links */
.nav-links ul li a::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -5px;
  width: 0%;
  height: 2px;
  background: linear-gradient(45deg, #835aff, #5ec8f7);
  transition: width 0.3s ease-in-out;
}

.nav-links ul li a:hover::after {
  width: 100%;
}

/* Burger Menu Styling */
.burger {
  display: none;
  cursor: pointer;
  flex-direction: column;
  justify-content: space-around;
  width: 30px;
  height: 21px;
  background: none;
  border: none;
}

.burger-line {
  width: 100%;
  height: 3px;
  background: #ffffff;
  transition: all 0.3s ease-in-out;
}

.burger:hover .burger-line {
  background: #5ec8f7;
}

/* Mobile & Dynamic Island Support */
@media screen and (max-width: 768px) {
  .burger {
    display: flex;
  }

  .nav-links {
    position: absolute;
    top: 50px;
    left: 0;
    width: 100%;
    height: 0;
    overflow: hidden;
    background: rgba(0, 0, 0, 0.9);
    flex-direction: column;
    align-items: center;
    transition: transform 0.5s ease;
  }

  .nav-links ul {
    flex-direction: column;
    gap: 15px;
  }

  .nav-links.nav-active {
    height: auto;
    transform: translateY(0%);
    opacity: 1;
  }
}
</style>
