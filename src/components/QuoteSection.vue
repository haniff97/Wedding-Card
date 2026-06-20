<template>
  <section class="section quote-section">
    <div class="elegant-border fade-in-scroll">
      <div class="quote-container reveal-on-scroll text-center">
        <img src="../assets/flower.png" class="flower-icon" alt="Flower icon" />
        
        <p class="arabic-text">
          وَمِنْ ءَايَٰتِهِۦٓ أَنْ خَلَقَ لَكُم مِّنْ أَنفُسِكُمْ أَزْوَٰجًا لِّتَسْكُنُوٓا۟ إِلَيْهَا وَجَعَلَ بَيْنَكُم مَّوَدَّةً وَرَحْمَةً ۚ إِنَّ فِى ذَٰلِكَ لَءَايَٰتٍ لِّقَوْمٍ يَتَفَكَّرُونَ
        </p>
        
        <p class="translation serif">
          "Dan di antara tanda-tanda kekuasaan-Nya ialah Dia menciptakan untukmu berpasang-pasangan dari jenismu sendiri, supaya kamu merasa tenang dan tenteram kepadanya, dan dijadikan-Nya diantaramu rasa kasih dan sayang. Sesungguhnya pada yang demikian itu benar-benar terdapat tanda-tanda bagi kaum yang berfikir."
        </p>
        
        <p class="surah uppercase">
          (QS. Ar-Rum: 21)
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.quote-section {
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

.quote-container {
  max-width: 600px;
  width: 100%;
  margin: 0 auto;
  position: relative;
  z-index: 10;
}

.flower-icon {
  width: 40px;
  margin: 0 auto 2rem auto;
  mix-blend-mode: multiply;
  opacity: 0.7;
  display: block;
}

.arabic-text {
  font-size: 1.8rem;
  line-height: 2.2;
  color: var(--color-primary-dark);
  margin-bottom: 2rem;
  font-family: 'Amiri', 'Traditional Arabic', serif;
}

.translation {
  font-size: 1rem;
  line-height: 1.8;
  font-style: italic;
  color: var(--color-text);
  margin-bottom: 2rem;
}

.surah {
  color: var(--color-gold);
  font-size: 0.9rem;
  letter-spacing: 2px;
}

@media (max-width: 600px) {
  .elegant-border {
    padding: 2rem 1rem;
  }
  
  .arabic-text {
    font-size: 1.5rem;
    line-height: 2;
  }
  
  .translation {
    font-size: 0.95rem;
  }
}
</style>
