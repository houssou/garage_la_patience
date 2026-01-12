<template>
  <div class="allContent">
    <!-- Navigation -->
    <nav :class="['navbar', { 'navbar-scrolled': scrolled }]">
      <div class="nav-container">
        <div class="nav-header">
          <div class="logo-wrapper">
            <div class="logo">
              <img src="../src/assets/logo.png" alt="" />
            </div>
            <!-- <div class="logo-text">
              <div class="logo-title">LA PATIENCE</div>
              <div class="logo-subtitle">RÉPARATION AUTO - GARAGE</div>
            </div> -->
          </div>

          <!-- Desktop Menu -->
          <ul class="desktop-menu">
            <li v-for="item in menuItems" :key="item">
              <button
                @click="scrollToSection(item)"
                :class="['menu-btn', { active: activeSection === item }]"
              >
                {{ item }}
              </button>
            </li>
          </ul>

          <!-- Mobile Menu Button -->
          <button @click="isMenuOpen = !isMenuOpen" class="mobile-menu-btn">
            <XIcon v-if="isMenuOpen" :size="32" />
            <MenuIcon v-else :size="32" />
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <div v-if="isMenuOpen" class="mobile-menu">
        <ul class="mobile-menu-list">
          <li v-for="item in menuItems" :key="item">
            <button @click="scrollToSection(item)" class="mobile-menu-btn">
              {{ item }}
            </button>
          </li>
        </ul>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="accueil" class="hero-section">
      <div class="hero-main">
        <!-- Animated Background -->
        <div class="hero-bg">
          <div class="bg-circle bg-circle-1"></div>
          <div class="bg-circle bg-circle-2"></div>
        </div>

        <div class="hero-content">
          <h1 class="hero-title">
            GARAGE <span class="hero-title-highlight">LA PATIENCE</span>
          </h1>
          <p class="hero-subtitle">Mécanique générale - Depuis 1988</p>
          <p class="hero-description">
            Votre partenaire de confiance pour l’entretien et la réparation de
            véhicules toutes marques. Service professionnel, rapide et garanti.
          </p>
          <div class="hero-buttons">
            <button @click="scrollToSection('contact')" class="btn-primary">
              Prendre Rendez-vous
            </button>
            <button @click="scrollToSection('services')" class="btn-secondary">
              Nos Services
            </button>
          </div>
        </div>

        <!-- Scroll Indicator -->
        <div class="scroll-indicator">
          <div class="scroll-indicator-outer">
            <div class="scroll-indicator-inner"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section id="services" class="services-section">
      <div class="section-container">
        <div class="section-header">
          <h2 class="section-title">Nos Services</h2>
          <div class="section-divider"></div>
        </div>

        <div class="services-grid">
          <div
            v-for="(service, index) in services"
            :key="index"
            class="service-card"
            @mouseover="hoveredService = index"
            @mouseleave="hoveredService = -1"
          >
            <div class="service-icon">
              <component :is="service.icon" />
            </div>
            <h3 class="service-title">{{ service.title }}</h3>
            <p class="service-description">
              {{ service.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Team Section -->
    <section id="équipe" class="team-section">
      <div class="section-container">
        <div class="section-header">
          <h2 class="section-title">Notre Équipe Administrative</h2>
          <div class="section-divider"></div>
          <p class="section-subtitle">Des professionnels à votre service</p>
        </div>

        <div class="team-grid">
          <div v-for="(member, index) in team" :key="index" class="team-card">
            <div class="team-member-avatar">
              <UserIcon class="avatar-icon" />
            </div>
            <h3 class="team-member-name">
              {{ member.name }}
            </h3>
            <p class="team-member-role">
              {{ member.role }}
            </p>
            <div class="team-member-info">
              <!-- <div class="info-item">
                <PhoneIcon class="info-icon" />
                <span>{{ member.phone }}</span>
              </div> -->
              <!-- <div class="info-item">
                <MailIcon class="info-icon" />
                <span>{{ member.email }}</span>
              </div> -->
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Gallery Section -->
    <section id="galerie" class="gallery-section">
      <div class="section-container">
        <div class="section-header">
          <h2 class="section-title">Notre Galerie</h2>
          <div class="section-divider"></div>
        </div>

        <div class="gallery-grid">
          <div
            v-for="(item, index) in galleryItems"
            :key="index"
            class="gallery-item"
            :class="`gallery-item-${index + 1}`"
          >
            <img :src="item.img" :alt="item.title" class="gallery-image" />
            <div class="gallery-overlay">
              <h3 class="gallery-item-title">
                {{ item.title }}
              </h3>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact-section">
      <div class="section-container">
        <div class="section-header">
          <h2 class="section-title">Contact & Itinéraire</h2>
          <div class="section-divider"></div>
        </div>

        <div class="contact-grid">
          <!-- Contact Info -->
          <div class="contact-info">
            <h3 class="contact-info-title">Coordonnées</h3>

            <div class="contact-details">
              <div class="contact-item">
                <MapPinIcon class="contact-icon" />
                <div>
                  <p class="contact-label">Adresse</p>
                  <p class="contact-value">
                    C.Lot 1201 Ahuansori - Toweta2<br />6ème Arrondissement,
                    Cotonou, République du Benin
                  </p>
                </div>
              </div>

              <div class="contact-item">
                <PhoneIcon class="contact-icon" />
                <div>
                  <p class="contact-label">Téléphone</p>
                  <p class="contact-value">01 97 33 57 80</p>
                </div>
              </div>

              <div class="contact-item">
                <MailIcon class="contact-icon" />
                <div>
                  <p class="contact-label">Email</p>
                  <p class="contact-value">garagelapatience1988@gmail.com</p>
                </div>
              </div>

              <div class="contact-item">
                <ClockIcon class="contact-icon" />
                <div>
                  <p class="contact-label">Horaires</p>
                  <p class="contact-value">Lundi - Vendredi: 8h00 - 18h00</p>
                  <p class="contact-value">Samedi: 9h00 - 18h00</p>
                  <p class="contact-value">Dimanche: Fermé</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Map Placeholder -->
          <div class="map-placeholder">
            <div class="map-content">
              <!-- <MapPinIcon class="map-icon" />
              <p class="map-text">Carte Google Maps</p> -->
              <p class="map-subtext">
                <iframe
                  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3965.0536814762086!2d2.426016975712753!3d6.387074224732211!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x1023555a360db91b%3A0xa60ee9b98a1eee09!2sGarage%20la%20patience!5e0!3m2!1sfr!2sbj!4v1768124220899!5m2!1sfr!2sbj"
                  style="border: 0"
                  allowfullscreen=""
                  loading="lazy"
                  referrerpolicy="no-referrer-when-downgrade"
                   class="map-iframe"
                ></iframe>
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <FloatingButtons />
    <!-- Footer -->
    <footer class="footer">
      <div class="footer-content">
        <div class="footer-logo">
          <div class="footer-title">GARAGE LA PATIENCE</div>
          <div class="footer-subtitle">Mécanique générale - Depuis 1988</div>
        </div>
        <p class="footer-copyright">
          © 2026 Garage La Patience - Tous droits réservés, Developpé par
          <a href="https://www.wyreel.com"> WYREEL GROUPE</a>
        </p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import {
  Wrench as WrenchIcon,
  Settings as SettingsIcon,
  Car as CarIcon,
  Battery as BatteryIcon,
  Shield as ShieldIcon,
  Snowflake as SnowflakeIcon,
  Hammer as HammerIcon,
  Paintbrush as PaintbrushIcon,
  Zap as ZapIcon,
  Cpu as CpuIcon,
  Droplets as DropletsIcon,
  Fuel as FuelIcon,
  Menu as MenuIcon,
  X as XIcon,
  Phone as PhoneIcon,
  Mail as MailIcon,
  MapPin as MapPinIcon,
  Clock as ClockIcon,
  User as UserIcon,
} from "lucide-vue-next";

// Import du composant FloatingButtons
import FloatingButtons from "./components/FloatingButtons.vue";

// State
const isMenuOpen = ref(false);
const scrolled = ref(false);
const activeSection = ref("accueil");
const hoveredService = ref(-1);

// Data
const menuItems = ["accueil", "services", "équipe", "galerie", "contact"];

const services = [
  {
    icon: WrenchIcon,
    title: "Entretien & Révision",
    description:
      "Vidange, contrôle technique, révision complète selon le carnet d'entretien",
  },
  {
    icon: SettingsIcon,
    title: "Mécanique Générale",
    description: "Diagnostic et réparation moteur, transmission, embrayage",
  },
  {
    icon: CarIcon,
    title: "Pneumatiques",
    description: "Montage, équilibrage, permutation et vente de pneus",
  },
  {
    icon: BatteryIcon,
    title: "Électricité Auto",
    description: "Diagnostic électronique et système électrique",
  },
  {
    icon: ShieldIcon,
    title: "Freinage",
    description: "Contrôle et remplacement plaquettes, disques",
  },
  {
    icon: SnowflakeIcon,
    title: "Climatisation",
    description: "Recharge et réparation système climatisation",
  },
  {
    icon: HammerIcon,
    title: "Tôlerie",
    description: "Réparation de carrosserie, débosselage sans peinture",
  },
  {
    icon: PaintbrushIcon,
    title: "Peinture Auto",
    description: "Peinture carrosserie, retouche et protection de la peinture",
  },
  {
    icon: ZapIcon,
    title: "Électricité & Électronique",
    description: "Système électrique, éclairage, circuits électroniques",
  },
  {
    icon: CpuIcon,
    title: "Programmation & Diagnostique",
    description: "Programmation calculateurs, diagnostique électronique avancé",
  },
  {
    icon: DropletsIcon,
    title: "Lavage & Nettoyage",
    description:
      "Lavage extérieur, nettoyage intérieur, traitement de la carrosserie",
  },
  {
    icon: FuelIcon,
    title: "Carburant & Injection",
    description: "Nettoyage injecteurs, système carburant, pompe à essence",
  },
];

const team = [
  {
    name: "HOUSSOU HOUNYO Médard Lie",
    role: "Directeur Général",
    phone: "01 97 33 57 80",
    email: "",
  },
  {
    name: "HOUSSOU HOUNYO James Arnold",
    role: "Chef d'Atelier et Responsable Administratif",
    phone: "01 23 45 67 91",
    email: "",
  },
  {
    name: "DOSSOU YOVO Germain",
    role: "Comptable et Responsable Financier",
    phone: "01 23 45 67 91",
    email: "",
  },
  {
    name: "HOUSSOU HOUNYO Oriana",
    role: "Secrétaire et Responsable Commerciale",
    phone: "01 23 45 67 92",
    email: "",
  },
];

const galleryItems = [
  {
    title: "Atelier Moderne",
    img: "/images/atelier1.jpeg",
  },
  {
    title: "Équipement Pro",
    img: "/images/atelier2.jpeg",
  },
  {
    title: "Zone Accueil",
    img: "/images/atelier3.jpeg",
  },
  {
    title: "Diagnostic",
    img: "/images/atelier4.jpeg",
  },
  {
    title: "Espace Pneus",
    img: "/images/atelier5.jpeg",
  },
  {
    title: "Notre Équipe",
    img: "/images/atelier1.jpeg", // Note: corrigé pour utiliser une image différente
  },
];

// Methods
const scrollToSection = (id) => {
  const element = document.getElementById(id);
  if (element) {
    element.scrollIntoView({ behavior: "smooth" });
    isMenuOpen.value = false;
    activeSection.value = id;
  }
};

const handleScroll = () => {
  scrolled.value = window.scrollY > 50;
};

// Lifecycle
onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style>
/* Reset et styles de base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  width: 100vw;
  height: 100vh;
  overflow-x: hidden;
}
button:focus {
  border: none !important;
  outline: none !important;
}
#app {
  max-width: 100% !important;
  margin: 0 !important;
  padding: 0px;
  text-align: center;
}
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, sans-serif;
  line-height: 1.6;
  color: #333;
}
/* .icon{
  width: 30px !important;
  height: 30px !important;
} */
.container {
  min-height: 100vh;
  background-color: #f8fafc;
}

/* Navigation */
.navbar {
  position: fixed;
  width: 100%;
  left: 0px;
  z-index: 50;
  transition: all 0.3s ease;
  background-color: rgb(255, 255, 255);
  backdrop-filter: blur(8px);
}

.navbar-scrolled {
  background-color: #ffffff;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}

/* Conteneur vidéo principal */
.video-container {
  position: relative;
  width: 100%;

  margin: 40px auto 0;
  background-color: #000; /* Fond noir pour éviter les bordures blanches */
  border-radius: 8px; /* Coins arrondis optionnels */
  overflow: hidden; /* Pour que l'iframe respecte les coins arrondis */
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15); /* Ombre optionnelle */
}

/* Iframe vidéo */
.video-iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 0;
  display: block;
}

/* Pour le responsive design */
@media (max-width: 768px) {
  .video-container {
    max-width: 95%; /* Prend plus de largeur sur mobile */
    margin: 30px auto 0;
    border-radius: 4px; /* Coins moins arrondis sur mobile */
  }
}

/* Pour les très petits écrans */
@media (max-width: 480px) {
  .video-container {
    margin: 20px auto 0;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1); /* Ombre plus légère */
  }
}

/* Variante avec aspect ratio différent (optionnelle) */
.video-container-16-9 {
  padding-bottom: 56.25%; /* Ratio 16:9 (9/16 = 0.5625) */
}

.video-container-4-3 {
  padding-bottom: 75%; /* Ratio 4:3 (3/4 = 0.75) */
}

.video-container-1-1 {
  padding-bottom: 100%; /* Ratio carré 1:1 */
}

/* Classes utilitaires pour les marges */
.video-container.mt-small {
  margin-top: 20px;
}

.video-container.mt-medium {
  margin-top: 40px;
}

.video-container.mt-large {
  margin-top: 60px;
}

/* Pour une vidéo avec légende/titre */
.video-with-caption {
  margin-bottom: 60px;
}

.video-caption {
  text-align: center;
  margin-top: 15px;
  font-style: italic;
  color: #666;
  font-size: 0.9rem;
}

/* Effet de survol (optionnel) */
.video-container:hover {
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
  transform: translateY(-2px);
  transition: all 0.3s ease;
}

.video-container {
  transition: all 0.3s ease;
}

.mobile-menu-btn svg {
  width: 40px !important; /* Taille de l'icône */
  height: 40px !important; /* Taille de l'icône */
  stroke-width: 2.5px !important; /* Épaisseur du trait */
}

/* Optionnel: animation au survol */
.mobile-menu-btn:hover svg {
  transform: scale(1.1);
  transition: transform 0.2s ease;
}

.allContent {
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  position: relative;
}

.nav-container {
  width: 100%;
  margin: 0 auto;
  padding: 0.75rem 1.5rem;
  max-width: 1280px ;
}

.nav-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo-wrapper {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo img {
  width: 90px;
  height: auto;
  filter: drop-shadow(0 10px 15px rgba(0, 0, 0, 0.1));
}

.gear-bg {
  fill: #1e293b;
  stroke: #3b82f6;
  stroke-width: 3;
}

.gear-teeth {
  fill: #3b82f6;
}

.gear-center {
  fill: #ef4444;
}

.wrench {
  fill: white;
}

.logo-text {
  display: flex;
  flex-direction: column;
}

.logo-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
  line-height: 1.2;
}

.logo-subtitle {
  font-size: 0.75rem;
  color: #60a5fa;
  font-weight: 600;
  letter-spacing: 0.1em;
}





.mobile-menu-list li .mobile-menu-btn{
  color: #fff !important
}


.footer-copyright a {
  color: #fff;
  font-size: 12px;

}

.map-content {
  width: 100%;
  height: 100%;
  position: relative;
  min-height: 450px;
}

.map-container {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 300px; /* Hauteur minimale */
}

.map-iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 0;
}









.desktop-menu {
  display: none;
  list-style: none;
  gap: 2rem;
}

@media (min-width: 768px) {
  .desktop-menu {
    display: flex;
  }
}

.menu-btn {
  background: none;
  border: none;
  color: #0f172a;
  text-transform: capitalize;
  font-weight: 500;
  font-size: 1rem;
  cursor: pointer;
  transition: color 0.2s ease;
}

@media (max-width: 768px) {
  .contact-grid{
    width: 100px;
  }
  .map-placeholder {
    padding: 10px !important;
    width: calc(100vw - 3rem) !important;
  }
  .contact-info {
    padding: 15px !important; /* Augmenté de 2px à 15px */
      width: calc(100vw - 3rem) !important;
  }
  /* .map-content .map-subtext iframe{
    width: 600px !important;
    height: 450px !important;
  }
  .map-content{
    width: 600px !important;
    height: 450px !important;
  } */
}

.menu-btn:hover {
  color: #f87171;
}

.menu-btn.active {
  color: #f87171;
}

.mobile-menu-btn {
  display: block;
  background: none;
  border: none;
  color: #0f172a !important;
  cursor: pointer;
  padding: 0.5rem;
  display: flex;
}

@media (min-width: 768px) {
  .mobile-menu-btn {
    display: none;
  }
}

.icon {
  width: 30px;
  height: 30px;
}

.mobile-menu {
  background-color: rgba(15, 23, 42, 0.98);
  backdrop-filter: blur(12px);
}


@media (min-width: 768px) {
  .mobile-menu {
    display: none;
  }
  .mobile-menu-btn {
    display: none !important;
  }
}

.mobile-menu-list {
  list-style: none;
  padding: 1rem 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.mobile-menu-btn {
  background: none;
  border: none;
  text-transform: capitalize;
  font-weight: 500;
  font-size: 1rem;
  cursor: pointer;
  transition: color 0.2s ease;
  text-align: left;
  width: 30px;
  padding: 0.5rem 0;
  color: #0f172a !important;
  cursor: pointer;
  padding: 0.5rem;
  display: flex;
}

.mobile-menu-btn:hover {
  color: #f87171;
}

/* Hero Section */
.hero-section {
  min-height: 100vh;
  width: calc(100vw - 1rem);

  position: relative;
  overflow: hidden;
  background-image: url("../src/assets/bg.jpeg");
  background-size: cover;
}
.hero-main {
  position: relative;
  min-height: 100vh;
  width: calc(100vw - 1rem);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;

  background: linear-gradient(
    135deg,
    #0f172a79 0%,
    #1e3b8a86 50%,
    #0f172a83 100%
  );

  padding: 2rem 1.5rem;
}

.hero-bg {
  position: absolute;
  inset: 0;
  opacity: 0.2;
}

.bg-circle {
  position: absolute;
  border-radius: 50%;
  filter: blur(48px);
}

.bg-circle-1 {
  top: 5rem;
  left: 5rem;
  width: 18rem;
  height: 18rem;
  background-color: #dc2626;
  animation: pulse 2s ease-in-out infinite;
}

.bg-circle-2 {
  bottom: 5rem;
  right: 5rem;
  width: 24rem;
  height: 24rem;
  background-color: #2563eb;
  animation: pulse 2s ease-in-out infinite 0.7s;
}

@keyframes pulse {
  0%,
  100% {
    opacity: 0.2;
    transform: scale(1);
  }
  50% {
    opacity: 0.3;
    transform: scale(1.05);
  }
}

.hero-content {
  position: relative;
  z-index: 10;
  text-align: center;
  max-width: 80rem;
  margin: 0 auto;
}

.hero-logo {
  margin-bottom: 2rem;
}

.hero-logo-svg {
  width: 150px;
  height: 150px;
  margin: 0 auto;
  filter: drop-shadow(0 25px 25px rgba(0, 0, 0, 0.25));
}

.hero-gear-bg {
  fill: #1e293b;
  stroke: #3b82f6;
  stroke-width: 3;
}

.hero-gear-teeth {
  fill: #3b82f6;
}

.hero-gear-center {
  fill: #ef4444;
}

.hero-wrench {
  fill: white;
}

.hero-title {
  font-size: 3rem;
  font-weight: bold;
  color: white;
  margin-bottom: 1rem;
  animation: fadeIn 1s ease-out;
}

@media (min-width: 768px) {
  .hero-title {
    font-size: 4rem;
  }
}

@media (min-width: 1024px) {
  .hero-title {
    font-size: 6rem;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero-title-highlight {
  background: linear-gradient(to right, #ef4444, #dc2626);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.hero-subtitle {
  font-size: 1.125rem;
  color: #93c5fd;
  font-weight: 600;
  margin-bottom: 0.5rem;
  letter-spacing: 0.05em;
}

@media (min-width: 768px) {
  .hero-subtitle {
    font-size: 1.25rem;
  }
}

.hero-description {
  font-size: 1.25rem;
  color: #cbd5e1;
  margin-bottom: 3rem;
  max-width: 42rem;
  margin-left: auto;
  margin-right: auto;
}

@media (min-width: 768px) {
  .hero-description {
    font-size: 1.5rem;
  }
}

.hero-buttons {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  justify-content: center;
}

@media (min-width: 640px) {
  .hero-buttons {
    flex-direction: row;
  }
}

.btn-primary,
.btn-secondary {
  padding: 1rem 2rem;
  border-radius: 9999px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  border: none;
}

.btn-primary {
  background: linear-gradient(to right, #dc2626, #b91c1c);
  color: white;
}

.btn-primary:hover {
  box-shadow: 0 25px 50px -12px rgba(220, 38, 38, 0.25);
  transform: scale(1.05);
}

.btn-secondary {
  background-color: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(8px);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.2);
}

.btn-secondary:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%,
  100% {
    transform: translateX(-50%) translateY(0);
  }
  50% {
    transform: translateX(-50%) translateY(-10px);
  }
}

.scroll-indicator-outer {
  width: 1.5rem;
  height: 2.5rem;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 9999px;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding: 0.5rem;
}

.scroll-indicator-inner {
  width: 0.25rem;
  height: 0.75rem;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 9999px;
}

/* Section communes */
.section-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 6rem 1.5rem;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 3rem;
  font-weight: bold;
  color: #0f172a;
  margin-bottom: 1rem;
}

@media (min-width: 1024px) {
  .section-title {
    font-size: 3.75rem;
  }
}

.section-divider {
  width: 6rem;
  height: 0.25rem;
  background: linear-gradient(to right, #2563eb, #dc2626);
  margin: 0 auto;
  border-radius: 9999px;
}

.section-subtitle {
  color: #64748b;
  font-size: 1.125rem;
  margin-top: 1rem;
}

/* Services Section */
.services-section {
  background-color: white;
}

.services-grid {
  display: grid;
  gap: 2rem;
}

@media (min-width: 768px) {
  .services-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .services-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.service-card {
  padding: 2rem;
  border-radius: 1rem;
  background: linear-gradient(135deg, #f8fafc, #e2e8f0);
  border: 2px solid transparent;
  cursor: pointer;
  transition: all 0.3s ease;
}

.service-card:hover {
  background: linear-gradient(135deg, #0f172a, #1e3a8a);
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  transform: translateY(-0.5rem);
  border-color: #3b82f6;
}

.service-icon {
  color: #dc2626;
  margin-bottom: 1rem;
  transition: color 0.3s ease;
}

.service-card:hover .service-icon {
  color: #f87171;
}

.service-icon svg {
  width: 3rem;
  height: 3rem;
}

.service-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #0f172a;
  margin-bottom: 0.75rem;
  transition: color 0.3s ease;
}

.service-card:hover .service-title {
  color: white;
}

.service-description {
  color: #64748b;
  transition: color 0.3s ease;
}

.service-card:hover .service-description {
  color: #cbd5e1;
}

/* Team Section */
.team-section {
  background-color: #f8fafc;
}

.team-grid {
  display: grid;
  gap: 2rem;
}

@media (min-width: 768px) {
  .team-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .team-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}

.team-card {
  background-color: white;
  padding: 2rem;
  border-radius: 1rem;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  /* border-top: 4px solid #2563eb; */
}

.team-card:hover {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  transform: translateY(-0.5rem);
}

.team-member-avatar {
  width: 5rem;
  height: 5rem;
  background: linear-gradient(135deg, #2563eb, #dc2626);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1rem auto;
}

.avatar-icon {
  width: 2.5rem;
  height: 2.5rem;
  color: white;
}

.team-member-name {
  font-size: 1.25rem;
  font-weight: bold;
  color: #0f172a;
  text-align: center;
  margin-bottom: 0.5rem;
}

.team-member-role {
  color: #dc2626;
  font-weight: 600;
  text-align: center;
  margin-bottom: 1rem;
}

.team-member-info {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  font-size: 0.875rem;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #64748b;
}

.info-icon {
  width: 1rem;
  height: 1rem;
  color: #2563eb;
}

/* Gallery Section */
.gallery-section {
  background-color: white;
}

.gallery-grid {
  display: grid;
  gap: 1.5rem;
}

@media (min-width: 768px) {
  .gallery-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .gallery-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.gallery-item {
  position: relative;
  height: 16rem;
  border-radius: 1rem;
  overflow: hidden;
  cursor: pointer;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}
.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.gallery-item:hover {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  transform: scale(1.02);
}

.gallery-item-1 {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
}
.gallery-item-2 {
  background: linear-gradient(135deg, #dc2626, #b91c1c);
}
.gallery-item-3 {
  background: linear-gradient(135deg, #3b82f6, #4f46e5);
}
.gallery-item-4 {
  background: linear-gradient(135deg, #ef4444, #f97316);
}
.gallery-item-5 {
  background: linear-gradient(135deg, #475569, #1e293b);
}
.gallery-item-6 {
  background: linear-gradient(135deg, #1d4ed8, #dc2626);
}

.gallery-overlay {
  position: absolute;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s ease;
}

.gallery-item:hover .gallery-overlay {
  background-color: rgba(0, 0, 0, 0.6);
}

.gallery-item-title {
  color: white;
  font-size: 1.5rem;
  font-weight: bold;
  transition: transform 0.3s ease;
}

.gallery-item:hover .gallery-item-title {
  transform: scale(1.1);
}

/* Contact Section */
.contact-section {
  background-color: #f8fafc;
}

.contact-grid {
  display: grid;
  gap: 3rem;
}

@media (min-width: 1024px) {
  .contact-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

.contact-info {
  background: linear-gradient(135deg, #0f172a, #1e3a8a);
  padding: 2.5rem;
  border-radius: 1.5rem;
  color: white;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}

.contact-info-title {
  font-size: 1.875rem;
  font-weight: bold;
  color: #f87171;
  margin-bottom: 2rem;
  text-align: left;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-item {
  display: flex;
  gap: 1rem;
  justify-content: flex-start;
}

.contact-icon {
  width: 1.5rem;
  height: 1.5rem;
  color: #f87171;
  flex-shrink: 0;
  margin-top: 0.25rem;
}

.contact-label {
  font-weight: 600;
  font-size: 1.125rem;
  margin-bottom: 0.25rem;
  text-align: left;
}

.contact-value {
  color: #cbd5e1;
  text-align: left;
}

.map-placeholder {
  background: linear-gradient(135deg, #f1f5f9, #e2e8f0);
  border-radius: 1.5rem;
  padding: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}

.map-content {
  text-align: center;

}

.map-icon {
  width: 4rem;
  height: 4rem;
  color: #94a3b8;
  margin: 0 auto 1rem auto;
}

.map-text {
  color: #475569;
  font-size: 1.125rem;
  font-weight: 500;
}

.map-subtext {
  color: #64748b;
  font-size: 0.875rem;
  margin-top: 0.5rem;
}

/* Footer */
.footer {
  background-color: #0f172a;
  color: white;
  padding: 2rem 1.5rem;
  text-align: center;
}

.footer-content {
  max-width: 1280px;
  margin: 0 auto;
}

.footer-logo {
  margin-bottom: 1rem;
}

.footer-title {
  font-size: 1.25rem;
  font-weight: bold;
  color: #f87171;
}

.footer-subtitle {
  font-size: 0.75rem;
  color: #60a5fa;
  letter-spacing: 0.1em;
}

.footer-copyright {
  color: #94a3b8;
}
</style>