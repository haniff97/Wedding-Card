<template>
  <section class="section hero-section">
    <!-- Decorative flowers outside stacking context -->
    <img src="../assets/flower.png" class="flower top-left flower-reveal" alt="Flower decoration" />
    <img src="../assets/flower.png" class="flower bottom-right flower-reveal" alt="Flower decoration" />

    <!-- Thin elegant border inside the section -->
    <div class="elegant-border fade-in-scroll">
      
      <div class="hero-content reveal-on-scroll">
        <p class="uppercase subtitle">Sebuah Perjalanan Bermula</p>
        
        <div class="names-wrapper">
          <h1 class="names">Hanini</h1>
          <span class="ampersand serif">&amp;</span>
          <h1 class="names">Haniff</h1>
        </div>
        
        <div class="date-container">
          <span class="date serif">06 . 09 . 2026</span>
        </div>
        
        <p class="quote serif">
          "Dan Kami jadikan kamu berpasang - pasangan"<br/>
          <span class="surah uppercase">Surah An-Naba' (78:8)</span>
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  background: var(--color-bg);
  /* Optional watercolor effect background */
  background-image: linear-gradient(180deg, #f5edf1 0%, #fdfbf7 50%, #fdfbf7 100%);
}

.elegant-border {
  width: 100%;
  height: 100%;
  border: 1px solid var(--color-gold);
  border-radius: 100px 100px 4px 4px; /* Arch effect */
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 3rem 1rem;
}

.hero-content {
  text-align: center;
  z-index: 10;
  max-width: 90%;
  position: relative;
}

.subtitle {
  color: var(--color-text);
  margin-bottom: 2rem;
  letter-spacing: 4px;
}

.names-wrapper {
  margin: 2rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.names {
  font-size: 6rem;
  line-height: 0.7;
  color: var(--color-primary);
  text-shadow: 1px 1px 2px rgba(212, 122, 158, 0.1);
  font-weight: 400;
  transform: rotate(-3deg);
}

.ampersand {
  font-size: 2.5rem;
  color: var(--color-gold);
  margin: 1.5rem 0;
  font-style: italic;
  font-weight: 300;
}

.date-container {
  margin: 3rem 0;
}

.date {
  font-size: 1.2rem;
  letter-spacing: 6px;
  color: var(--color-text);
  border-bottom: 1px solid var(--color-gold);
  padding-bottom: 0.5rem;
}

.quote {
  font-style: italic;
  font-size: 0.9rem;
  margin-top: 3rem;
  color: #8c8588;
  line-height: 1.8;
}

.surah {
  font-size: 0.7rem;
  font-weight: 400;
  color: var(--color-gold);
  display: block;
  margin-top: 0.5rem;
}

/* Flowers */
.flower {
  position: absolute;
  mix-blend-mode: multiply;
  opacity: 0.6;
  filter: blur(2px);
  z-index: 1;
}

.top-left {
  top: -40px;
  left: -40px;
  width: 280px;
  transform: rotate(110deg);
}

.bottom-right {
  bottom: -30px;
  right: -30px;
  width: 320px;
}

@media (max-width: 600px) {
  .names {
    font-size: 4.5rem;
  }
  .elegant-border {
    border-radius: 80px 80px 4px 4px;
  }
}
</style>
