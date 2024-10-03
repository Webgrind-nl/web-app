<template>
  <div class="hero">
    <h1>Jouw <span>Toekomst</span>, Onze Innovatie</h1>
    <p>Van visionaire ideeën tot sterke realisaties: wij bouwen de digitale basis voor jouw groei</p>
    <a href="#services" class="btn" @click="scrollToServices">Bekijk Onze Diensten</a>
  </div>
</template>

<script setup>
const scrollToServices = () => {
  const servicesSection = document.querySelector("#services");
  if (servicesSection) {
    servicesSection.scrollIntoView({ behavior: "smooth" });
  }
};
</script>

<style scoped>
/* The existing hero and button styles */
.hero {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 20px;
    height: 100vh;
    padding: 0 20px;
    margin: 0 auto;
}

.hero h1 {
    font-size: 3rem;
    margin-bottom: 20px;
    color: white;
    animation: fadeIn 1.5s ease-out;
}

.hero p {
    font-size: 1.2rem;
    margin-bottom: 40px;
    color: white;
    animation: fadeIn 2s ease-out;
}

.hero span {
    background: linear-gradient(135deg, #6a0dad, #d16ba5, #45aaf2); /* Initial gradient */
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-size: 100%;
    transition: background-size 10s ease, transform 0.8s ease; /* Slow gradient transition via background-size */
}

.hero span:hover {
    background: linear-gradient(135deg, #9a4fda, #e89ac4, #7cc4f5); /* Lighter gradient on hover */
    background-size: 200%; /* Change the size for a smooth transition */
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    transform: scale(1.05); /* Slightly scale up the text on hover */
}

.btn {
    background: linear-gradient(135deg, #6a0dad, #d16ba5, #45aaf2);
    color: white;
    padding: 14px 36px;
    font-size: 1.1rem;
    border: none;
    border-radius: 50px;
    text-decoration: none;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    transition: background 1.2s ease, transform 0.4s ease, box-shadow 0.4s ease;
    cursor: pointer;
}

.btn:hover {
    transform: translateY(-5px) scale(1.05);
    box-shadow: 0 6px 15px rgba(0, 0, 0, 0.3);
}

.hero h1, .hero p {
    transition: color 0.3s ease, transform 0.3s ease;
}

.hero h1:hover, .hero p:hover {
    color: white;
    transform: translateY(-5px);
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@media (max-width: 900px) {
    .hero h1 {
        font-size: 2rem;
    }

    .hero p {
        font-size: 1.2rem;
    }

    .btn {
        padding: 10px 20px;
        font-size: 0.9rem;
    }
}

@media (max-width: 480px) {
    .hero h1 {
        font-size: 2rem;
    }

    .hero p {
        font-size: 0.9rem;
    }
}
</style>
