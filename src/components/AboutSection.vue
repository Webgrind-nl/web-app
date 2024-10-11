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
      <h1 class="title">{{ service.title }}</h1>
      <p>{{ service.description }}</p>
    </div>

    <!-- Modal for displaying more information -->
    <div v-if="modalService" class="modal-overlay" @click.self="closeModal">
      <div
        class="modal-content"
        :class="{ 'elegant-pop-up': isOpen, 'elegant-pop-close': isClosing }"
      >
        <button class="close-button" @click="closeModal">&times;</button>
        <div class="modal-icon animate-3d">{{ modalService.icon }}</div>
        <h2>{{ modalService.title }}</h2>
        <p>{{ modalService.fullDescription }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";

const services = [
  {
    title: "Webontwikkeling",
    description: "Ontwikkelen van responsieve en robuuste websites.",
    icon: "🌐",
    fullDescription:
      "Wij zijn gespecialiseerd in het bouwen van schaalbare, SEO-vriendelijke en visueel aantrekkelijke websites die volledig zijn afgestemd op jouw bedrijfsdoelen. Onze weboplossingen zorgen voor optimale prestaties op elk apparaat, zodat jouw online aanwezigheid sterk en gebruiksvriendelijk is.",
  },
  {
    title: "Mobiele Apps",
    description: "Ontwikkelen van gebruiksvriendelijke mobiele applicaties.",
    icon: "📱",
    fullDescription:
      "Ons team ontwikkelt krachtige mobiele apps met naadloze gebruikerservaringen, gericht op zowel Android- als iOS-platforms. Van concept tot publicatie zorgen wij ervoor dat jouw app gebruiksvriendelijk, intuïtief en geoptimaliseerd is voor maximale prestaties.",
  },
  {
    title: "UI/UX Ontwerp",
    description: "Creëren van boeiende gebruikerservaringen.",
    icon: "🎨",
    fullDescription:
      "Wij richten ons op het ontwerpen van intuïtieve UI/UX-interfaces die zorgen voor een aantrekkelijke en gebruiksvriendelijke ervaring. Ons ontwerpteam werkt nauw samen met jou om de perfecte balans te vinden tussen esthetiek en functionaliteit, zodat jouw digitale product naadloos aansluit bij de behoeften van jouw gebruikers.",
  },
  {
    title: "SEO Optimalisatie",
    description: "Verbeteren van zichtbaarheid in zoekmachines.",
    icon: "🚀",
    fullDescription:
      "Onze SEO-diensten helpen jouw website hoger te scoren in zoekmachines zoals Google, wat resulteert in meer organisch verkeer en een grotere online zichtbaarheid. We implementeren strategieën op maat, zoals technische optimalisaties, contentcreatie en linkbuilding, om jouw bedrijf te laten opvallen in de zoekresultaten.",
  },
  {
    title: "Cloudoplossingen",
    description: "Implementeren van schaalbare cloudinfrastructuren.",
    icon: "☁️",
    fullDescription:
      "Wij bieden betrouwbare en schaalbare cloudoplossingen die de prestaties van jouw bedrijf naar een hoger niveau tillen. Of het nu gaat om dataopslag, serverbeheer of cloudmigratie, wij zorgen voor veilige en efficiënte cloudinfrastructuren die voldoen aan jouw bedrijfsbehoeften. Onze cloudoplossingen zorgen ervoor dat jouw applicaties soepel draaien en eenvoudig kunnen worden opgeschaald bij groei.",
  },
  {
    title: "IT-Consultancy",
    description: "Verstrekken van strategisch IT-advies.",
    icon: "💡",
    fullDescription:
      "Wij bieden strategisch IT-advies om jouw bedrijf te helpen slimme technologische beslissingen te nemen. Of het nu gaat om het optimaliseren van bestaande systemen, het implementeren van nieuwe technologieën of het waarborgen van IT-beveiliging, ons team van experts staat klaar om jou te ondersteunen. We helpen je bij het opstellen van een toekomstbestendige IT-strategie die jouw bedrijfsdoelstellingen ondersteunt.",
  },
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

<style>
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
  background: linear-gradient(0deg, #181a35, #2a2c5c);
  color: white;
  text-align: center;
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.15);
  opacity: 0;
  transform: scale(1) translateY(50px) rotate(0deg);
  cursor: pointer;

  transition: transform 0.5s ease, box-shadow 0.5s ease, opacity 1s ease;
}

.service-cards-container .service-card:hover {
  transform: scale(1.02) translateY(-10px); /* Increase size significantly */
  box-shadow: 0 25px 45px rgba(131, 90, 255, 0.4); /* Bigger shadow */
  z-index: 2; /* Bring it to the front */
}

/* Smooth Appear Animation */
.service-card.visible {
  opacity: 1;
  transform: scale(1) translateY(0) rotate(0deg);
}

/* Floating Effect */
@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translatey(-10px);
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

.title {
  background: linear-gradient(
    135deg,
    #9a4fda,
    #e89ac4,
    #7cc4f5
  ); /* Gradient colors */
  -webkit-background-clip: text; /* Clip the background to text for Webkit browsers */
  background-clip: text; /* Standard background clip */
  color: transparent; /* Make text color transparent to show gradient */
  font-size: 24px;
}
</style>
