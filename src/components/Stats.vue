<template>
  <section class="section pengurus" id="pengurus">
    <div class="container">
      <div 
        class="stats-content"
        v-motion
        :initial="{ opacity: 0, y: 50 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="200"
      >
        <div class="stats-header">
          <h2>Pengurus Koperasi</h2>
          <p>Para pengurus yang menjalankan roda organisasi koperasi dengan penuh dedikasi</p>
        </div>

        <!-- Grid untuk foto pengurus koperasi -->
        <div class="pengurus-grid">
          <div 
            v-for="(pengurus, index) in pengurusList"
            :key="pengurus.id"
            class="pengurus-item"
            v-motion
            :initial="{ opacity: 0, y: 30 }"
            :enter="{ opacity: 1, y: 0 }"
            :delay="400 + (index * 100)"
          >
            <div class="pengurus-image-container">
              <img 
                :src="pengurus.image" 
                :alt="pengurus.name"
                class="pengurus-image"
                @error="handleImageError"
              />
              <div class="pengurus-overlay">
                <div class="pengurus-name">{{ pengurus.name }}</div>
                <div class="pengurus-position">{{ pengurus.position }}</div>
              </div>
            </div>
            <div class="pengurus-content">
              <h3 class="pengurus-name-mobile">{{ pengurus.name }}</h3>
              <p class="pengurus-position-mobile">{{ pengurus.position }}</p>
              <p class="pengurus-bio">{{ pengurus.bio }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Pengurus {
  id: number
  name: string
  position: string
  bio: string
  image: string
}

const pengurusList: Pengurus[] = [
  {
    id: 1,
    name: 'Khaidir Anwar Sani, S.IP',
    position: 'Ketua Koperasi',
    bio: 'Berpengalaman dalam manajemen koperasi selama lebih dari 10 tahun',
    image: '/pengurus/ketuakop.png' 
  },
  {
    id: 2,
    name: 'Astri Munggarani, S.I.Kom',
    position: 'Sekretaris',
    bio: 'Berpengalaman dalam administrasi dan pengelolaan organisasi',
    image: '/pengurus/sekretaris.png' 
  },
  {
    id: 3,
    name: 'Muhammad Anggi Natapraja, S.Pi',
    position: 'Bendahara',
    bio: 'Ahli dalam pengelolaan keuangan koperasi syariah',
    image: '/pengurus/bendahara.png'
  }
]

const handleImageError = (event: Event) => {
  const target = event.target as HTMLImageElement;
  target.src = '/default-avatar.png'; // Fallback image jika gambar tidak ditemukan
}
</script>

<style scoped>
.stats {
  background: var(--gray-light);
  position: relative;
  overflow: hidden;
  padding: 4rem 0;
}

.stats::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="dots" width="20" height="20" patternUnits="userSpaceOnUse"><circle cx="10" cy="10" r="1" fill="rgba(10,29,55,0.05)"/></pattern></defs><rect width="100" height="100" fill="url(%23dots)"/></svg>');
}

.stats-content {
  position: relative;
  z-index: 2;
}

.stats-header {
  text-align: center;
  margin-bottom: 4rem;
}

.stats-header h2 {
  color: var(--primary-color);
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.stats-header p {
  color: var(--gray-medium);
  font-size: 1.2rem;
}

.pengurus-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.pengurus-item {
  background: var(--white);
  border-radius: 16px;
  box-shadow: var(--shadow);
  overflow: hidden;
  transition: all 0.3s ease;
  position: relative;
}

.pengurus-item:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-hover);
}

.pengurus-image-container {
  position: relative;
  overflow: hidden;
  height: 300px;
}

.pengurus-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.pengurus-item:hover .pengurus-image {
  transform: scale(1.05);
}

.pengurus-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
  color: white;
  padding: 2rem 1.5rem 1rem;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}

.pengurus-item:hover .pengurus-overlay {
  transform: translateY(0);
}

.pengurus-name {
  font-size: 1.4rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.pengurus-position {
  font-size: 1rem;
  color: #ddd;
}

.pengurus-content {
  padding: 1.5rem;
  text-align: center;
}

.pengurus-name-mobile {
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--primary-color);
  margin: 0 0 0.5rem 0;
  display: none;
}

.pengurus-position-mobile {
  color: var(--accent-color);
  font-weight: 500;
  margin-bottom: 1rem;
  display: none;
}

.pengurus-bio {
  color: var(--gray-medium);
  font-size: 0.95rem;
  line-height: 1.6;
}

@media (max-width: 768px) {
  .stats-header h2 {
    font-size: 2rem;
  }
  
  .pengurus-grid {
    grid-template-columns: 1fr;
  }
  
  .pengurus-overlay {
    transform: translateY(0); /* Tampilkan info di mobile */
  }
  
  .pengurus-name-mobile, 
  .pengurus-position-mobile {
    display: block;
  }
  
  .pengurus-overlay {
    display: none; /* Sembunyikan overlay di mobile karena info ditampilkan di bawah */
  }
}
</style>