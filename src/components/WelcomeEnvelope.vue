<template>
  <div class="envelope-wrapper" :class="{ 'is-open': isOpen, 'is-hidden': isHidden }">
    <div class="envelope" @click="openEnvelope">
      <div class="envelope-flap"></div>
      <div class="envelope-body">
        <div class="guest-info fade-in">
          <p class="uppercase serif to-text">Kepada</p>
          <h2 class="guest-name">{{ guestName }}</h2>
          <p class="tap-text uppercase">Klik Untuk Buka</p>
        </div>
        <img src="../assets/flower.png" class="envelope-flower" alt="Flower decoration" />
      </div>
    </div>
  </div>
  
  <div class="main-content" :class="{ 'content-visible': isOpen }">
    <slot></slot>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const isOpen = ref(false);
const isHidden = ref(false);
const guestName = ref('Tetamu Jemputan');

onMounted(() => {
  // Extract 'to' parameter from URL for guest personalization
  const urlParams = new URLSearchParams(window.location.search);
  const toParam = urlParams.get('to');
  if (toParam) {
    guestName.value = toParam;
  }
});

const openEnvelope = () => {
  if (isOpen.value) return;
  isOpen.value = true;
  
  // Hide envelope from DOM completely after animation
  setTimeout(() => {
    isHidden.value = true;
  }, 1500); // Wait for slide-up animation to finish
};
</script>

<style scoped>
.envelope-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: var(--color-bg);
  z-index: 1000;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: transform 1s cubic-bezier(0.4, 0, 0.2, 1) 0.5s; /* Slide up after flap opens */
  background-image: radial-gradient(#d5c4be 1px, transparent 1px);
  background-size: 20px 20px;
}

.envelope-wrapper.is-open {
  transform: translateY(-100vh);
}

.envelope-wrapper.is-hidden {
  display: none;
}

.envelope {
  position: relative;
  width: 90%;
  max-width: 500px;
  aspect-ratio: 1.5;
  height: auto;
  background-color: var(--color-primary-light);
  border: 1px solid var(--color-gold);
  border-radius: 8px;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
  cursor: pointer;
  transition: transform 0.3s ease;
}

.envelope:hover {
  transform: scale(1.02);
}

/* Envelope Flap Top */
.envelope-flap {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 35%; /* Reduced to give maximum room for text */
  background-color: var(--color-primary-light);
  border-bottom: 1px solid var(--color-gold);
  border-right: 1px solid var(--color-gold);
  transform-origin: top;
  clip-path: polygon(0 0, 50% 100%, 100% 0);
  z-index: 3;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: inset 0 -5px 15px rgba(0,0,0,0.05);
}

.is-open .envelope-flap {
  transform: rotateX(180deg);
  z-index: 1; /* Move behind the body */
}

/* Envelope Body Bottom */
.envelope-body {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #fdfbf7;
  clip-path: polygon(0 100%, 0 0, 50% 35%, 100% 0, 100% 100%); /* Matches the 35% flap */
  z-index: 2;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  padding-bottom: 2rem;
  border-radius: 8px;
}

.guest-info {
  position: relative; /* Fix z-index not applying */
  text-align: center;
  z-index: 10;
}

.to-text {
  color: var(--color-gold);
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  letter-spacing: 2px;
}

.guest-name {
  font-size: 2.5rem;
  color: var(--color-primary-dark);
  font-family: var(--font-heading);
  text-shadow: 1px 1px 2px rgba(0,0,0,0.05);
  margin-bottom: 1rem;
}

.tap-text {
  font-size: 0.7rem;
  color: var(--color-text);
  letter-spacing: 2px;
  animation: pulse 2s infinite;
  background-color: rgba(255,255,255,0.8);
  padding: 4px 12px;
  border-radius: 20px;
  border: 1px solid var(--color-gold);
}

.envelope-flower {
  position: absolute;
  bottom: -20px;
  left: -20px;
  width: 150px;
  opacity: 0.5;
  mix-blend-mode: multiply;
  z-index: 1;
}

@keyframes pulse {
  0% { opacity: 0.6; transform: scale(0.95); }
  50% { opacity: 1; transform: scale(1.05); }
  100% { opacity: 0.6; transform: scale(0.95); }
}

@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

.fade-in {
  animation: fade-in 1.5s ease-out forwards;
}

.main-content {
  opacity: 0;
  visibility: hidden;
  height: 100vh;
  overflow: hidden;
  transition: opacity 1s ease 0.5s;
}

.main-content.content-visible {
  opacity: 1;
  visibility: visible;
  height: auto;
  overflow: visible;
}

@media (max-width: 600px) {
  .envelope-body {
    padding-bottom: 1rem;
  }
  .guest-name {
    font-size: 2.2rem;
    margin-bottom: 0.5rem;
  }
}
</style>
