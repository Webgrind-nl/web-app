<template>
  <div class="service-cards-container">
    <div
      class="service-card"
      v-for="(service, index) in services"
      :key="index"
      ref="cards"
      @click="openModal(service, $event)"
    >
      <div class="icon animate-3d">{{ service.icon }}</div>
      <h3>{{ service.title }}</h3>
      <p>{{ service.description }}</p>
    </div>

    <!-- Modal for displaying more information -->
    <div v-if="modalService" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content" :class="{'elegant-pop-up': isOpen, 'elegant-pop-close': isClosing}">
        <button class="close-button" @click="closeModal">&times;</button>
        <div class="modal-icon animate-3d">{{ modalService.icon }}</div>
        <h2>{{ modalService.title }}</h2>
        <p>{{ modalService.fullDescription }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue';

const services = [
  {
    title: "Web Development",
    description: "Building responsive and robust websites.",
    icon: "🌐",
    fullDescription: "We specialize in creating highly scalable, SEO-friendly, and visually appealing websites tailored to your needs."
  },
  {
    title: "Mobile Apps",
    description: "Developing intuitive mobile applications.",
    icon: "📱",
    fullDescription: "Our team develops powerful mobile apps with seamless user experiences, targeting both Android and iOS platforms."
  },
  {
    title: "UI/UX Design",
    description: "Crafting engaging user experiences.",
    icon: "🎨",
    fullDescription: "We focus on intuitive UI/UX design, ensuring that your customers have a delightful experience navigating your products."
  },
  {
    title: "SEO Optimization",
    description: "Improving search engine visibility.",
    icon: "🚀",
    fullDescription: "Our SEO services help your website rank higher, driving organic traffic and boosting your online presence."
  },
  {
    title: "Cloud Solutions",
    description: "Deploying scalable cloud infrastructures.",
    icon: "☁️",
    fullDescription: "We offer reliable and scalable cloud infrastructure solutions, ensuring smooth performance for your business."
  },
  {
    title: "IT Consulting",
    description: "Providing strategic IT advice.",
    icon: "💡",
    fullDescription: "We provide IT consulting services to help businesses make informed technology decisions."
  }
];

const modalService = ref(null);
const isOpen = ref(false);
const isClosing = ref(false);

const openModal = (service) => {
  modalService.value = service;
  isOpen.value = true;
  isClosing.value = false;
};

const closeModal = () => {
  isClosing.value = true;
  isOpen.value = false;
  
  setTimeout(() => {
    modalService.value = null;
    isClosing.value = false; // Reset after animation ends
  }, 600); // Match the duration of the closing animation
};

onMounted(() => {
  const cards = document.querySelectorAll(".service-card");
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add("visible");
        observer.unobserve(entry.target);
      }
    });
  });

  cards.forEach((card) => observer.observe(card));
});
</script>

<style scoped>
/* Container Styling */
.service-cards-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 40px;
  margin: 40px auto;
  padding: 20px;
  max-width: 1200px;
}

/* Service Card Styling */
.service-card {
  flex: 1 1 calc(48%);
  max-width: 550px;
  padding: 40px;
  border-radius: 15px;
  background: linear-gradient(135deg, #6a0dad, #d16ba5, #45aaf2);
  color: white;
  text-align: center;
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.15);
  opacity: 0;
  transform: scale(0.9) translateY(50px) rotate(-2deg);
  transition: opacity 1s ease, transform 1s ease, box-shadow 0.3s ease;
  cursor: pointer;
}

/* Hover Effect */
.service-card:hover {
  transform: scale(1.05) translateY(0);
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.3);
}

/* Visible Class for Scroll Animation */
.service-card.visible {
  opacity: 1;
  transform: scale(1) translateY(0) rotate(0deg);
  animation: float 3s ease-in-out infinite;
}

/* Floating Effect */
@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

/* 3D Rotation for Emoji */
.animate-3d {
  display: inline-block;
  font-size: 70px; /* Bigger emoji */
  animation: rotate3D 6s infinite linear;
}

/* 3D Rotation Keyframes */
@keyframes rotate3D {
  0% {
    transform: rotateX(0) rotateY(0);
  }
  50% {
    transform: rotateX(0deg) rotateY(90deg);
  }
  100% {
    transform: rotateX(0deg) rotateY(0deg);
  }
}

/* Modal Styling */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background: white;
  padding: 40px;
  border-radius: 10px;
  max-width: 600px;
  text-align: center;
  position: relative;
}

/* Elegant Pop-up Animation */
.elegant-pop-up {
  animation: elegantPopUp 0.6s ease-out forwards;
}

.elegant-pop-close {
  animation: elegantPopClose 0.6s ease-out forwards;
}

@keyframes elegantPopUp {
  0% {
    transform: scale(0.8) translateY(20px);
    opacity: 0;
  }
  100% {
    transform: scale(1) translateY(0);
    opacity: 1;
  }
}

@keyframes elegantPopClose {
  0% {
    transform: scale(1) translateY(0);
    opacity: 1;
  }
  100% {
    transform: scale(0.8) translateY(20px);
    opacity: 0;
  }
}

.modal-icon {
  font-size: 70px;
  margin-bottom: 20px;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 15px;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
}

.close-button:hover {
  color: red;
}
</style>
