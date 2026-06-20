<template>
  <section class="section rsvp-section">
    <!-- Thin elegant border inside the section -->
    <div class="elegant-border fade-in-scroll">
      <div class="rsvp-container reveal-on-scroll">
        <h2 class="section-title text-center">Kehadiran Tetamu</h2>
        <p class="subtitle text-center serif uppercase">RSVP</p>
        
        <div class="divider">
          <span class="line"></span>
          <img src="../assets/flower.png" class="flower-icon" alt="Flower icon" />
          <span class="line"></span>
        </div>
        
        <p class="text-center notice serif">Mohon kesudian anda untuk mengisi maklumat</br>kehadiran dan ucapan buat pasangan pengantin di</br>bawah:</p>
        
        <form @submit.prevent="submitRsvpToWhatsApp" class="rsvp-form">
          <div class="form-group">
            <label for="name" class="uppercase">Nama Penuh</label>
            <input type="text" id="name" v-model="formData.name" required placeholder="Masukkan nama anda" />
          </div>
          
          <div class="form-group">
            <label for="attendance" class="uppercase">Kehadiran</label>
            <select id="attendance" v-model="formData.attendance" required>
              <option value="" disabled>Pilih status kehadiran</option>
              <option value="Hadir">Hadir</option>
              <option value="Tidak Hadir">Tidak Hadir</option>
            </select>
          </div>
          
          <div class="form-group" v-if="formData.attendance === 'Hadir'">
            <label for="guests" class="uppercase">Jumlah Kehadiran (Sekeluarga)</label>
            <input type="number" id="guests" v-model="formData.guests" min="1" max="15" placeholder="Contoh: 4" required />
          </div>
          
          <div class="form-group">
            <label for="wishes" class="uppercase">Ucapan</label>
            <textarea id="wishes" v-model="formData.wishes" rows="3" placeholder="Tinggalkan ucapan untuk pengantin"></textarea>
          </div>
          
          <div class="text-center action-area">
            <button type="submit" class="submit-btn whatsapp-btn">
              <span class="icon">💬</span> Hantar RSVP WhatsApp
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive } from 'vue';

const formData = reactive({
  name: '',
  attendance: '',
  guests: '1',
  meal: '',
  wishes: ''
});

// Using a placeholder number. Replace with real phone number.
const whatsappNumber = "60173289264";

const submitRsvpToWhatsApp = () => {
  let message = `Assalamualaikum. Saya *${formData.name}* ingin mengesahkan bahawa saya *${formData.attendance}* ke majlis perkahwinan Hanini & Haniff.`;
  
  if (formData.attendance === 'Hadir') {
    message += `\n\n*Bilangan Kehadiran:* ${formData.guests} Orang`;
    if (formData.meal) {
      message += `\n*Nota Makanan:* ${formData.meal}`;
    }
  }
  
  if (formData.wishes) {
    message += `\n\n*Ucapan:* "${formData.wishes}"`;
  }
  
  const encodedMessage = encodeURIComponent(message);
  const whatsappUrl = `https://wa.me/${whatsappNumber}?text=${encodedMessage}`;
  
  window.open(whatsappUrl, '_blank');
};
</script>

<style scoped>
.rsvp-section {
  background-color: var(--color-bg);
  padding-bottom: 4rem; /* Extra space at the bottom of the page */
}

@media (max-width: 600px) {
  .rsvp-section {
    padding-bottom: 6rem;
  }
}

.elegant-border {
  width: 100%;
  height: 100%;
  border: 1px solid var(--color-gold);
  border-radius: 4px 4px 100px 100px; /* Arch effect at the bottom */
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 4rem 1rem 6rem 1rem;
}

.rsvp-container {
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  position: relative;
  z-index: 10;
}

.section-title {
  font-size: 3rem;
  color: var(--color-primary-dark);
  margin-bottom: 0.2rem;
}

.subtitle {
  color: var(--color-gold);
  letter-spacing: 4px;
}

.divider {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2rem 0;
}

.line {
  width: 50px;
  height: 1px;
  background-color: var(--color-gold);
  opacity: 0.5;
}

.flower-icon {
  width: 30px;
  margin: 0 1rem;
  mix-blend-mode: multiply;
  opacity: 0.7;
}

.notice {
  margin-bottom: 2.5rem;
  color: var(--color-text);
}

.form-group {
  margin-bottom: 1.5rem;
  text-align: left;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  color: var(--color-gold);
  font-size: 0.75rem;
  letter-spacing: 2px;
}

.action-area {
  margin-top: 3rem;
}

.submit-btn {
  width: 100%;
  max-width: 350px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  margin: 0 auto;
  padding: 1.2rem;
  border-radius: 50px;
  font-family: var(--font-body);
  font-weight: 600;
  font-size: 1rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: none;
  cursor: pointer;
}

.whatsapp-btn {
  background: linear-gradient(135deg, #25D366, #128C7E);
  color: white;
  box-shadow: 0 8px 25px rgba(37, 211, 102, 0.3);
}

.whatsapp-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 12px 30px rgba(37, 211, 102, 0.4);
}

.whatsapp-btn .icon {
  font-size: 1.4rem;
}

@media (max-width: 600px) {
  .elegant-border {
    padding: 2rem 1rem 5rem 1rem;
    border-radius: 4px 4px 80px 80px;
  }
  
  .submit-btn {
    padding: 1rem;
    font-size: 0.85rem;
    max-width: 280px;
  }
  
  .whatsapp-btn .icon {
    font-size: 1.2rem;
  }
}
</style>
