<template>
  <div class="countdown-container fade-in-scroll">
    <div class="elegant-border">
      <h3 class="countdown-title uppercase serif text-center">Menghitung Hari</h3>
      <div class="countdown-boxes">
        <div class="time-box">
          <span class="number serif">{{ days }}</span>
          <span class="label uppercase">Hari</span>
        </div>
        <div class="time-box">
          <span class="number serif">{{ hours }}</span>
          <span class="label uppercase">Jam</span>
        </div>
        <div class="time-box">
          <span class="number serif">{{ minutes }}</span>
          <span class="label uppercase">Minit</span>
        </div>
        <div class="time-box">
          <span class="number serif">{{ seconds }}</span>
          <span class="label uppercase">Saat</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Target Date: 06 Sept 2026 11:00 AM
const targetDate = new Date('September 6, 2026 11:00:00').getTime();

const days = ref('00');
const hours = ref('00');
const minutes = ref('00');
const seconds = ref('00');

let timerInterval;

const updateCountdown = () => {
  const now = new Date().getTime();
  const distance = targetDate - now;

  if (distance < 0) {
    clearInterval(timerInterval);
    days.value = '00';
    hours.value = '00';
    minutes.value = '00';
    seconds.value = '00';
    return;
  }

  const d = Math.floor(distance / (1000 * 60 * 60 * 24));
  const h = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  const m = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  const s = Math.floor((distance % (1000 * 60)) / 1000);

  days.value = d.toString().padStart(2, '0');
  hours.value = h.toString().padStart(2, '0');
  minutes.value = m.toString().padStart(2, '0');
  seconds.value = s.toString().padStart(2, '0');
};

onMounted(() => {
  updateCountdown();
  timerInterval = setInterval(updateCountdown, 1000);
});

onUnmounted(() => {
  clearInterval(timerInterval);
});
</script>

<style scoped>
.countdown-container {
  width: 100%;
  padding: 0 1rem;
  margin: -2rem 0 3rem 0; /* Overlap slightly with hero section */
  position: relative;
  z-index: 20;
}

.elegant-border {
  background-color: var(--color-bg);
  border: 1px solid var(--color-gold);
  border-radius: 4px;
  padding: 2rem 1rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
  max-width: 450px;
  margin: 0 auto;
}

.countdown-title {
  color: var(--color-gold);
  font-size: 1rem;
  letter-spacing: 3px;
  margin-bottom: 1.5rem;
}

.countdown-boxes {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.time-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 70px;
  height: 70px;
  background-color: var(--color-primary-light);
  border-radius: 4px;
  border: 1px solid rgba(197, 160, 89, 0.3);
}

.number {
  font-size: 1.8rem;
  color: var(--color-primary-dark);
  line-height: 1;
  margin-bottom: 0.2rem;
}

.label {
  font-size: 0.6rem;
  color: var(--color-text);
  letter-spacing: 1px;
}

@media (max-width: 400px) {
  .countdown-boxes {
    gap: 0.5rem;
  }
  .time-box {
    width: 60px;
    height: 60px;
  }
  .number {
    font-size: 1.4rem;
  }
}
</style>
