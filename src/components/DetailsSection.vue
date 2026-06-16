<template>
  <section class="section details-section">
    <!-- Animated floral background outside stacking context -->
    <img src="../assets/flower.png" class="flower flower-reveal flower-bg-left" alt="Flower decoration" />
    <img src="../assets/flower.png" class="flower flower-reveal flower-bg-right" alt="Flower decoration" />

    <!-- Thin elegant border inside the section -->
    <div class="elegant-border fade-in-scroll">

      <div class="details-container reveal-on-scroll">
        <div class="bismillah text-center">
          <span class="bismillah-text">﷽</span>
        </div>
        
        <p class="greeting text-center serif">Assalamualaikum & Salam Sejahtera</p>
        
        <div class="parents text-center">
          <h3 class="parents-name uppercase">Hasnan Bin Abd Hamid</h3>
          <span class="ampersand serif">&amp;</span>
          <h3 class="parents-name uppercase">Hasnah Binti Sait</h3>
        </div>
        
        <p class="invitation-text text-center serif">
          Dengan penuh kesyukuran ke hadrat Ilahi, kami menjemput<br/>
          Dato'/ Datin/ Tuan/ Puan/ Encik/ Cik
        </p>
        
        <div class="divider">
          <span class="line"></span>
          <span class="text uppercase">ke majlis perkahwinan puteri kami</span>
          <span class="line"></span>
        </div>
        
        <div class="bride-groom text-center">
          <h2 class="name">Marisya Hanini Binti Hasnan</h2>
          <p class="with-love serif">dengan pilihan hatinya</p>
          <h2 class="name">Muhammad Haniff Bin Hamdan</h2>
        </div>

        <div class="event-details">
          <div class="date-box">
            <p class="day uppercase">Ahad</p>
            <p class="date-num serif">06</p>
            <p class="month uppercase">Sept 2026</p>
          </div>
          <div class="info-box">
            <div class="venue">
              <h4 class="uppercase">Inara Gerbang Hall</h4>
              <p class="serif">Lot 6589, Lorong Bakti, Jin Bawal,<br/>Kampung Sungai Udang,<br/>41250 Klang, Selangor</p>
            </div>
            <div class="itinerary">
              <h4 class="uppercase">Aturcara Majlis</h4>
              <p class="serif">Jamuan Makan : 11:00AM - 4:00PM<br/>Ketibaan Pengantin : 12:30PM</p>
            </div>
          </div>
        </div>

        <div class="action-buttons">
          <a href="https://maps.app.goo.gl/search/Inara+Gerbang+Hall" target="_blank" class="action-btn">
            <span class="icon">📍</span>
            <span class="uppercase">Google Maps</span>
          </a>
          <a href="https://waze.com/ul?q=Inara+Gerbang+Hall" target="_blank" class="action-btn">
            <span class="icon">🚗</span>
            <span class="uppercase">Waze</span>
          </a>
          <a :href="calendarUrl" target="_blank" class="action-btn">
            <span class="icon">📅</span>
            <span class="uppercase">Save the Date</span>
          </a>
          <button @click="shareLink" class="action-btn share-btn" v-if="canShare">
            <span class="icon">📤</span>
            <span class="uppercase">Share</span>
          </button>
        </div>
        
        <p class="footer-text text-center serif">
          Semoga dengan kehadiran para tetamu dapat menyerikan<br/>lagi hari bahagia puteri kami
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue';

// Generate Google Calendar Link
const calendarUrl = computed(() => {
  const text = encodeURIComponent("Majlis Perkahwinan Hanini & Haniff");
  const dates = "20260906T030000Z/20260906T080000Z"; // 11AM - 4PM GMT+8
  const details = encodeURIComponent("Walimatul Urus Marisya Hanini & Muhammad Haniff. Kehadiran anda amat dihargai.");
  const location = encodeURIComponent("Inara Gerbang Hall, Klang, Selangor");
  return `https://calendar.google.com/calendar/render?action=TEMPLATE&text=${text}&dates=${dates}&details=${details}&location=${location}`;
});

const canShare = !!navigator.share;

const shareLink = async () => {
  if (navigator.share) {
    try {
      await navigator.share({
        title: 'Walimatul Urus Hanini & Haniff',
        text: 'Kami menjemput anda ke majlis perkahwinan kami. Klik pautan untuk maklumat lanjut.',
        url: window.location.href,
      });
    } catch (err) {
      console.log('Error sharing:', err);
    }
  }
};
</script>

<style scoped>
.details-section {
  background-color: var(--color-bg);
}

.elegant-border {
  width: 100%;
  height: 100%;
  border: 1px solid var(--color-gold);
  border-radius: 4px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 4rem 2rem;
}

.details-container {
  width: 100%;
  max-width: 500px;
  position: relative;
  z-index: 10;
}

.bismillah-text {
  font-size: clamp(2rem, 12vw, 4rem);
  color: var(--color-gold);
  line-height: 1;
  display: block;
  margin-bottom: 1.5rem;
  opacity: 0.9;
}

.greeting {
  font-size: 1rem;
  margin-bottom: 2rem;
  font-style: italic;
  color: var(--color-primary-dark);
}

.parents-name {
  font-size: 1.1rem;
  color: var(--color-text);
  margin: 0.5rem 0;
  font-weight: 600;
}

.ampersand {
  font-size: 1.8rem;
  color: var(--color-gold);
  font-style: italic;
}

.invitation-text {
  margin: 2rem 0;
  font-size: 0.95rem;
  line-height: 1.8;
}

.divider {
  display: flex;
  align-items: center;
  margin: 2.5rem 0;
}

.line {
  flex: 1;
  height: 1px;
  background-color: var(--color-gold);
  opacity: 0.4;
}

.text {
  padding: 0 1rem;
  color: var(--color-gold);
  font-size: 0.75rem;
}

.bride-groom .name {
  font-size: 3rem;
  color: var(--color-primary);
  margin: 0.5rem 0;
  line-height: 1.2;
}

.with-love {
  font-size: 1rem;
  font-style: italic;
  color: var(--color-text);
  margin: 1.5rem 0;
}

.event-details {
  display: flex;
  border-top: 1px solid rgba(197, 160, 89, 0.3); /* Gold line */
  border-bottom: 1px solid rgba(197, 160, 89, 0.3);
  margin: 3rem 0;
  padding: 2rem 0;
}

.date-box {
  flex: 1;
  text-align: center;
  border-right: 1px solid rgba(197, 160, 89, 0.3);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-right: 1rem;
}

.date-box .day, .date-box .month {
  color: var(--color-gold);
}

.date-box .date-num {
  font-size: 3.5rem;
  line-height: 1;
  color: var(--color-primary-dark);
  margin: 0.5rem 0;
}

.info-box {
  flex: 2;
  padding-left: 2rem;
}

.venue {
  margin-bottom: 1.5rem;
}

.venue h4, .itinerary h4 {
  font-size: 0.9rem;
  color: var(--color-gold);
  margin-bottom: 0.5rem;
}

.venue p, .itinerary p {
  font-size: 0.9rem;
}

.action-buttons {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  margin: 3rem 0;
  width: 100%;
}

.action-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  background-color: #ffffff;
  color: var(--color-primary-dark);
  border: 1px solid var(--color-gold);
  padding: 1rem;
  border-radius: 50px; /* Pill shape */
  text-decoration: none;
  font-family: var(--font-body);
  font-weight: 600;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-size: 0.85rem;
  letter-spacing: 1px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.04);
}

.action-btn:hover {
  background-color: var(--color-primary);
  color: white;
  border-color: var(--color-primary);
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(212, 122, 158, 0.3);
}

.share-btn {
  width: 100%;
  cursor: pointer;
}

.action-btn .icon {
  font-size: 1.2rem;
  opacity: 0.8;
}

.footer-text {
  font-size: 0.9rem;
  font-style: italic;
  margin-top: 3rem;
  color: #8c8588;
}

/* Background Flowers */
.flower {
  position: absolute;
  mix-blend-mode: multiply;
  opacity: 0.3; /* Lighter inside the card */
  filter: blur(3px);
  z-index: 1;
}

.flower-bg-left {
  bottom: 5%;
  left: -40px;
  width: 250px;
  transform: rotate(45deg);
}

.flower-bg-right {
  top: 15%;
  right: -30px;
  width: 200px;
  transform: rotate(-120deg);
}

@media (max-width: 600px) {
  .elegant-border {
    padding: 3rem 1rem;
  }
  .event-details {
    flex-direction: column;
  }
  .date-box {
    border-right: none;
    border-bottom: 1px solid rgba(197, 160, 89, 0.3);
    padding-right: 0;
    padding-bottom: 1.5rem;
    margin-bottom: 1.5rem;
  }
  .info-box {
    padding-left: 0;
    text-align: center;
  }
  .action-buttons {
    grid-template-columns: 1fr;
    gap: 0.8rem;
  }
  .bride-groom .name {
    font-size: 2.5rem;
  }
}
</style>
