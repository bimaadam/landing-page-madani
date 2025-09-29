<template>
  <section id="beranda" class="hero">
    <div class="container">
      <div class="hero-content">
        <div 
          class="hero-text"
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :enter="{ opacity: 1, y: 0 }"
          :delay="200"
        >
          <h1 class="hero-title">
            Koperasi Athaya Raya Madani Bandung
            <span class="hero-subtitle">Solusi Simpan Pinjam & Pembiayaan yang Amanah</span>
          </h1>
          <p class="hero-description">
            Bergabunglah dengan koperasi terpercaya yang telah melayani ribuan anggota di Bandung. 
            Kami menyediakan layanan simpan pinjam yang syariah dan berbagai produk pembiayaan 
            yang sesuai dengan kebutuhan Anda.
          </p>
          <div class="hero-buttons">
            <a href="#kontak" class="btn btn-primary">Gabung Sekarang</a>
            <a href="#tentang" class="btn btn-secondary">Pelajari Lebih Lanjut</a>
          </div>
        </div>
        
        <div 
          class="hero-image"
          v-motion
          :initial="{ opacity: 0, x: 50 }"
          :enter="{ opacity: 1, x: 0 }"
          :delay="400"
        >
          <img src="/logoarm3d.png" alt="Koperasi Modern" />
        </div>
      </div>
    </div>
    
    <div class="hero-features">
      <div class="container">
        <div class="features-grid">
          <div 
            class="feature-item"
            v-motion
            :initial="{ opacity: 0, y: 30 }"
            :enter="{ opacity: 1, y: 0 }"
            :delay="600"
          >
            <div class="feature-icon">
              <IconMoneySave  />
            </div>
            <h3>Simpanan Aman</h3>
            <p>Simpanan Anda dijamin aman dengan bunga kompetitif</p>
          </div>
          
          <div 
            class="feature-item"
            v-motion
            :initial="{ opacity: 0, y: 30 }"
            :enter="{ opacity: 1, y: 0 }"
            :delay="700"
          >
            <div class="feature-icon">
              <IconBank />
            </div>
            <h3>Pinjaman Mudah</h3>
            <p>Proses pinjaman cepat dengan syarat yang fleksibel</p>
          </div>
          
          <div 
            class="feature-item"
            v-motion
            :initial="{ opacity: 0, y: 30 }"
            :enter="{ opacity: 1, y: 0 }"
            :delay="800"
          >
            <div class="feature-icon">
              <IconLayanan/>
            </div>
            <h3>Layanan Digital</h3>
            <p>Akses mudah melalui platform digital terpadu</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import IconMoneySave from './icons/IconMoneySave.vue';
import IconBank from './icons/IconBank.vue';
import IconLayanan from './icons/IconLayanan.vue';

// No additional script needed for this component
</script>

<style scoped>
.hero {
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--light-blue) 100%);
  color: var(--white);
  padding: 120px 0 80px;
  position: relative;
  overflow: hidden;
}

.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="grain" width="100" height="100" patternUnits="userSpaceOnUse"><circle cx="10" cy="10" r="1" fill="rgba(255,215,0,0.1)"/><circle cx="30" cy="30" r="1" fill="rgba(255,215,0,0.05)"/><circle cx="70" cy="20" r="1" fill="rgba(255,215,0,0.08)"/><circle cx="90" cy="80" r="1" fill="rgba(255,215,0,0.03)"/></pattern></defs><rect width="100" height="100" fill="url(%23grain)"/></svg>');
  opacity: 0.3;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  position: relative;
  z-index: 2;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 1rem;
}

.hero-subtitle {
  display: block;
  font-size: 1.5rem;
  font-weight: 500;
  color: var(--accent-color);
  margin-top: 0.5rem;
}

.hero-description {
  font-size: 1.1rem;
  margin-bottom: 2rem;
  opacity: 0.9;
  line-height: 1.6;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.hero-image img {
  width: 100%;
  max-width: 500px;
  border-radius: 16px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.hero-features {
  background: var(--white);
  margin-top: 80px;
  padding: 40px 0;
  border-radius: 20px 20px 0 0;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.feature-item {
  text-align: center;
  padding: 2rem;
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.feature-item h3 {
  color: var(--primary-color);
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.feature-item p {
  color: var(--gray-medium);
}

@media (max-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .hero-title {
    font-size: 2.2rem;
  }
  
  .hero-subtitle {
    font-size: 1.2rem;
  }
  
  .hero-buttons {
    justify-content: center;
  }
}
</style>