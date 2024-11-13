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
        :aria-expanded="menuOpen.toString()"
      >
        <span
          :class="{ 'burger-line': true, 'line-1': true, active: menuOpen }"
        ></span>
        <span
          :class="{ 'burger-line': true, 'line-2': true, active: menuOpen }"
        ></span>
        <span
          :class="{ 'burger-line': true, 'line-3': true, active: menuOpen }"
        ></span>
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

<script>
export default {
  data() {
    return {
      menuOpen: false,
    };
  },
  methods: {
    toggleMenu() {
      this.menuOpen = !this.menuOpen;
    },
  },
};
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

@media screen and (max-width: 768px) {
  /* Burger Menu Styling */
  .burger {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 35px;
    height: 30px;
    background: transparent;
    border: none;
    cursor: pointer;
    padding: 0;
    position: relative;
    z-index: 10;
    transition: transform 0.5s ease-in-out;
  }

  /* Hamburger Lines */
  .burger-line {
    width: 100%;
    height: 4px;
    background: linear-gradient(135deg, #9a4fda, #e89ac4, #7cc4f5);
    border-radius: 2px;
    position: relative;
    transition: transform 0.9s ease-in-out,
      /* Smooth transformation for all lines */ opacity 0.9s ease-in-out,
      /* Smooth opacity transition */ background-color 0.9s ease-in-out; /* Smooth color transition */
    will-change: transform, opacity, background-color; /* Hint the browser to optimize */
  }

  /* Line 1 Animation (Top Line) */
  .line-1.active {
    transform: translateY(11px) rotate(50deg); /* Move down and rotate */
    background: linear-gradient(
      -135deg,
      #9a4fda,
      #e89ac4,
      #7cc4f5
    ); /* Optional: Change color */
  }

  /* Line 2 Animation (Middle Line) */
  .line-2.active {
    opacity: 0; /* Fades out */
  }

  /* Line 3 Animation (Bottom Line) */
  .line-3.active {
    transform: translateY(-15px) rotate(-50deg); /* Move up and rotate */
    background: linear-gradient(
      135deg,
      #9a4fda,
      #e89ac4,
      #7cc4f5
    ); /* Optional: Change color */
  }

  /* .burger.active {
    transform: rotate(
      180deg
    );
  } */

  /* Hover Effect for Futuristic Feel */
  .burger:hover .burger-line {
    background: linear-gradient(
      135deg,
      #9a4fda,
      #e89ac4,
      #7cc4f5
    ); /* Neon-like color on hover */
    box-shadow: 0 0 15px rgba(154, 79, 218, 0.8),
      /* Purple from gradient */ 0 0 20px rgba(232, 154, 196, 0.6),
      /* Pinkish from gradient */ 0 0 25px rgba(124, 196, 245, 0.6); /* Light Blue from gradient */
    transition: box-shadow 0.05s ease-in-out,
      /* Smooth box-shadow transition */ background-color 0.1s ease-in-out; /* Smooth background-color change */
  }
}

/* Mobile & Dynamic Island Support */
@media screen and (max-width: 768px) {
  .burger {
    display: flex;
  }

  .nav-links {
    position: absolute;
    top: 0px;
    left: 0;
    width: 100%;
    height: 0;
    overflow: hidden;
    flex-direction: column;
    align-items: center;
    transition: transform 0.5s ease, backdrop-filter 0.05s ease;
  }

  .nav-links ul {
    flex-direction: column;
    gap: 15px;
  }

  .nav-links.nav-active {
    backdrop-filter: blur(5px);
    height: 100vh;
    transform: translateY(0%);
    opacity: 1;
    justify-content: center;
  }
}
</style>
