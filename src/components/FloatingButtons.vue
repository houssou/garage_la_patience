<template>
  <!-- Boutons flottants -->
  <div class="floating-buttons">
    <!-- Bouton WhatsApp -->
    <a 
      :href="whatsappLink"
      target="_blank"
      class="floating-button whatsapp-button"
      aria-label="Contactez-nous sur WhatsApp"
      @click="trackWhatsAppClick"
    >
      <svg class="button-icon" viewBox="0 0 24 24">
        <path fill="currentColor" d="M16.75 13.96c.25.13.41.2.46.3.06.11.04.61-.21 1.18-.2.56-1.24 1.1-1.7 1.12-.46.02-.47.36-2.96-.73-2.49-1.09-3.99-3.75-4.11-3.92-.12-.17-.96-1.38-.92-2.61.05-1.22.69-1.8.95-2.04.24-.26.51-.29.68-.26h.47c.15 0 .36-.06.55.45l.69 1.87c.06.13.1.28.01.44l-.27.41-.39.42c-.12.12-.26.25-.12.5.12.26.62 1.09 1.32 1.78.91.88 1.71 1.17 1.95 1.3.24.14.39.12.54-.04l.81-.94c.19-.25.35-.19.58-.11l1.67.88M12 2a10 10 0 0 1 10 10 10 10 0 0 1-10 10c-1.97 0-3.8-.57-5.35-1.55L2 22l1.55-4.65A9.96 9.96 0 0 1 2 12 10 10 0 0 1 12 2m0 2a8 8 0 0 0-8 8c0 1.72.54 3.31 1.46 4.61L4.5 19.5l2.89-.96A7.95 7.95 0 0 0 12 20a8 8 0 0 0 8-8 8 8 0 0 0-8-8z"/>
      </svg>
      <span class="button-text">WhatsApp</span>
    </a>
    
    <!-- Bouton YouTube -->
    <button 
      class="floating-button youtube-button"
      aria-label="Voir notre présentation"
      @click="openVideoModal"
    >
      <svg class="button-icon" viewBox="0 0 24 24">
        <path fill="currentColor" d="M10,15L15.19,12L10,9V15M21.56,7.17C21.69,7.64 21.78,8.27 21.84,9.07C21.91,9.87 21.94,10.56 21.94,11.16L22,12C22,14.19 21.84,15.8 21.56,16.83C21.31,17.73 20.73,18.31 19.83,18.56C19.36,18.69 18.5,18.78 17.18,18.84C15.88,18.91 14.69,18.94 13.59,18.94L12,19C7.81,19 5.2,18.84 4.17,18.56C3.27,18.31 2.69,17.73 2.44,16.83C2.31,16.36 2.22,15.73 2.16,14.93C2.09,14.13 2.06,13.44 2.06,12.84L2,12C2,9.81 2.16,8.2 2.44,7.17C2.69,6.27 3.27,5.69 4.17,5.44C4.64,5.31 5.5,5.22 6.82,5.16C8.12,5.09 9.31,5.06 10.41,5.06L12,5C16.19,5 18.8,5.16 19.83,5.44C20.73,5.69 21.31,6.27 21.56,7.17Z"/>
      </svg>
      <span class="button-text">Présentation</span>
    </button>
  </div>

  <!-- Modal pour la vidéo YouTube -->
  <div v-if="showVideoModal" class="video-modal" @click.self="closeVideoModal">
    <div class="modal-content">
      <button class="modal-close" @click="closeVideoModal" aria-label="Fermer">
        &times;
      </button>
      <div class="video-wrapper">
        <iframe 
          class="youtube-video"
          :src="`https://www.youtube.com/embed/${videoId}`"
          title="Présentation du Garage La Patience"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen
        ></iframe>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FloatingButtons',
  data() {
    return {
      showVideoModal: false,
      videoId: 'NYgRGOSBHek', // Remplacez par votre ID vidéo
      phoneNumber: '2290197335780', // Remplacez par votre numéro
      defaultMessage: 'Bonjour, je suis intéressé par vos services'
    };
  },
  computed: {
    whatsappLink() {
      const encodedMessage = encodeURIComponent(this.defaultMessage);
      return `https://wa.me/${this.phoneNumber}?text=${encodedMessage}`;
    }
  },
  methods: {
    openVideoModal() {
      this.showVideoModal = true;
      // Empêcher le scroll du body
      document.body.style.overflow = 'hidden';
    },
    closeVideoModal() {
      this.showVideoModal = false;
      // Restaurer le scroll
      document.body.style.overflow = 'auto';
    },
    trackWhatsAppClick() {
      // Ici vous pouvez ajouter du tracking analytics
      console.log('WhatsApp button clicked');
    }
  },
  mounted() {
    // Fermer le modal avec la touche Escape
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' && this.showVideoModal) {
        this.closeVideoModal();
      }
    });
  }
};
</script>

<style scoped>
.floating-buttons {
  position: fixed;
  bottom: 20px;
  right: 20px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  z-index: 1000;
}

.floating-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 20px;
  border-radius: 50px;
  border: none;
  font-weight: 600;
  font-size: 16px;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  min-width: 160px;
}

.whatsapp-button {
  background-color: #25D366;
  color: white;
}

.whatsapp-button:hover {
  background-color: #128C7E;
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

.youtube-button {
  background-color: #FF0000;
  color: white;
}

.youtube-button:hover {
  background-color: #CC0000;
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

.button-icon {
  width: 24px;
  height: 24px;
}

.button-text {
  white-space: nowrap;
}

/* Modal pour la vidéo */
.video-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
}

.modal-content {
  position: relative;
  width: 90%;
  max-width: 900px;
  background: #000;
  border-radius: 8px;
  overflow: hidden;
}

.modal-close {
  position: absolute;
  top: 10px;
  right: 10px;
  background: rgba(255, 255, 255, 0.2);
  border: none;
  color: white;
  font-size: 28px;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  transition: background 0.3s;
}

.modal-close:hover {
  background: rgba(255, 255, 255, 0.3);
}

.video-wrapper {
  position: relative;
  padding-bottom: 56.25%; /* Ratio 16:9 */
  height: 0;
}

.youtube-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/* Animation pour le modal */
.video-modal {
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Responsive */
@media (max-width: 768px) {
  .floating-buttons {
    bottom: 15px;
    right: 15px;
  }
  
  .floating-button {
    padding: 10px 16px;
    font-size: 14px;
    min-width: 140px;
  }
  
  .button-icon {
    width: 20px;
    height: 20px;
  }
  
  .modal-content {
    width: 95%;
  }
}

@media (max-width: 480px) {
  .floating-buttons {
    bottom: 10px;
    right: 10px;
    gap: 8px;
  }
  
  .floating-button {
    padding: 8px 12px;
    font-size: 13px;
    min-width: auto;
    width: 50px;
    height: 50px;
    border-radius: 50%;
  }
  
  .button-text {
    display: none;
  }
  
  .button-icon {
    width: 24px;
    height: 24px;
  }
}
</style>