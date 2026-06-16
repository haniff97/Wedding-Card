<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import WelcomeEnvelope from './components/WelcomeEnvelope.vue'
import HeroSection from './components/HeroSection.vue'
import CountdownTimer from './components/CountdownTimer.vue'
import DetailsSection from './components/DetailsSection.vue'
import RsvpForm from './components/RsvpForm.vue'

const scrollProgress = ref(0)
const circumference = 125.66 // 2 * PI * 20
const strokeDashoffset = computed(() => {
  return circumference - (scrollProgress.value / 100) * circumference
})

const updateScroll = () => {
  const winScroll = document.body.scrollTop || document.documentElement.scrollTop
  const height = document.documentElement.scrollHeight - document.documentElement.clientHeight
  scrollProgress.value = (winScroll / height) * 100
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => {
  window.addEventListener('scroll', updateScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateScroll)
})
</script>

<template>
  <div class="scroll-circle-container" @click="scrollToTop" :class="{ 'is-visible': scrollProgress > 5 }">
    <svg class="progress-ring" width="46" height="46">
      <circle class="progress-ring__circle-bg" stroke="rgba(197, 160, 89, 0.2)" stroke-width="2" fill="transparent" r="20" cx="23" cy="23"/>
      <circle class="progress-ring__circle" stroke="var(--color-gold)" stroke-width="2" fill="transparent" r="20" cx="23" cy="23"
        :style="{ strokeDasharray: circumference, strokeDashoffset: strokeDashoffset }"/>
    </svg>
    <span class="scroll-icon">↑</span>
  </div>
  
  <WelcomeEnvelope>
    <div class="invitation-wrapper">
      <main class="invitation-card">
        <HeroSection />
        <CountdownTimer />
        <DetailsSection />
        <RsvpForm />
      </main>
    </div>
  </WelcomeEnvelope>
</template>

<style>
.scroll-circle-container {
  position: fixed;
  bottom: 30px;
  right: 20px;
  width: 46px;
  height: 46px;
  z-index: 9999;
  cursor: pointer;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease, visibility 0.3s ease, transform 0.3s ease;
  transform: translateY(20px);
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(253, 251, 247, 0.9);
  border-radius: 50%;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
}

.scroll-circle-container.is-visible {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.scroll-circle-container:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 15px rgba(197, 160, 89, 0.2);
}

.progress-ring {
  position: absolute;
  top: 0;
  left: 0;
  transform: rotate(-90deg);
}

.progress-ring__circle {
  transition: stroke-dashoffset 0.1s ease;
  stroke-linecap: round;
}

.scroll-icon {
  color: var(--color-gold);
  font-size: 1.2rem;
  font-weight: 300;
  margin-top: -2px;
}
</style>

<style>
/* Global styles are imported via style.css in main.js */
main {
  width: 100%;
  overflow-x: hidden;
}
</style>
