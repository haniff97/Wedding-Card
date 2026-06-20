<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import WelcomeEnvelope from './components/WelcomeEnvelope.vue'
import HeroSection from './components/HeroSection.vue'
import QuoteSection from './components/QuoteSection.vue'
import CountdownTimer from './components/CountdownTimer.vue'
import DetailsSection from './components/DetailsSection.vue'
import RsvpForm from './components/RsvpForm.vue'
import MusicPlayer from './components/MusicPlayer.vue'

const musicPlayerRef = ref(null)
const activeSection = ref(0)
const isContentVisible = ref(false)

const sections = [
  { id: 'hero', label: 'Hero' },
  { id: 'quote', label: 'Quote' },
  { id: 'countdown', label: 'Countdown' },
  { id: 'details', label: 'Details' },
  { id: 'rsvp', label: 'RSVP' },
]

const onEnvelopeOpen = () => {
  isContentVisible.value = true
  if (musicPlayerRef.value) {
    musicPlayerRef.value.startMusic()
  }
}

const scrollToSection = (id) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const idx = sections.findIndex((s) => s.id === entry.target.id)
          if (idx !== -1) activeSection.value = idx
        }
      })
    },
    { threshold: 0.3 }
  )

  // Observe after a short delay to allow DOM to render
  setTimeout(() => {
    sections.forEach((s) => {
      const el = document.getElementById(s.id)
      if (el) observer.observe(el)
    })
  }, 2000)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<template>
  <!-- Dot navigation -->
  <div class="dot-nav" :class="{ 'is-visible': isContentVisible }">
    <button
      v-for="(section, idx) in sections"
      :key="section.id"
      class="dot"
      :class="{ active: activeSection === idx }"
      @click="scrollToSection(section.id)"
      :aria-label="'Go to ' + section.label"
    ></button>
  </div>

  <MusicPlayer ref="musicPlayerRef" />
  
  <WelcomeEnvelope @opened="onEnvelopeOpen">
    <div class="invitation-wrapper">
      <main class="invitation-card">
        <HeroSection id="hero" />
        <QuoteSection id="quote" />
        <CountdownTimer id="countdown" />
        <DetailsSection id="details" />
        <RsvpForm id="rsvp" />
      </main>
    </div>
  </WelcomeEnvelope>
</template>

<style>
.dot-nav {
  position: fixed;
  right: 24px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 9998;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 14px;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.5s ease, visibility 0.5s ease;
}

.dot-nav.is-visible {
  opacity: 1;
  visibility: visible;
}

/* Connecting line between dots */
.dot-nav::before {
  content: '';
  position: absolute;
  top: 5px;
  bottom: 5px;
  width: 1px;
  background-color: rgba(197, 160, 89, 0.35);
  z-index: -1;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: 1.5px solid var(--color-gold);
  background: rgba(253, 251, 247, 0.9);
  padding: 0;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  z-index: 1;
}

.dot:hover {
  background-color: rgba(197, 160, 89, 0.4);
  transform: scale(1.3);
}

.dot.active {
  background-color: var(--color-gold);
  transform: scale(1.3);
  box-shadow: 0 0 6px rgba(197, 160, 89, 0.5);
}

@media (max-width: 600px) {
  .dot-nav {
    right: 28px;
  }
  .dot {
    width: 8px;
    height: 8px;
  }
}
</style>

<style>
/* Global styles are imported via style.css in main.js */
main {
  width: 100%;
  overflow-x: hidden;
}
</style>
