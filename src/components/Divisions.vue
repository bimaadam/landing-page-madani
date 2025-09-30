<template>
  <section class="section divisions">
    <div class="container">
      <div 
        class="divisions-content"
        v-motion
        :initial="{ opacity: 0, y: 50 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="200"
      >
        <div class="divisions-header">
          <h2>Tim Divisi Koperasi</h2>
          <p>Para profesional yang mengelola setiap aspek operasional koperasi dengan kompeten</p>
        </div>

        <!-- Divisi Bisnis -->
        <div class="division-section">
          <h3 class="division-title">Divisi Bisnis</h3>
          <p class="division-description">
            Bertugas mengembangkan strategi bisnis, menjalin kemitraan, dan mencari peluang usaha baru
          </p>
          <div class="division-grid">
            <div 
              class="division-member"
              v-motion
              :initial="{ opacity: 0, y: 30 }"
              :enter="{ opacity: 1, y: 0 }"
              :delay="400"
            >
              <div class="member-image-container">
                <img 
                  :src="businessDivision.image" 
                  :alt="businessDivision.name"
                  class="member-image"
                  @error="handleImageError"
                />
                <div class="member-overlay">
                  <div class="member-name">{{ businessDivision.name }}</div>
                  <div class="member-position">{{ businessDivision.position }}</div>
                </div>
              </div>
              <div class="member-content">
                <h4 class="member-name-mobile">{{ businessDivision.name }}</h4>
                <p class="member-position-mobile">{{ businessDivision.position }}</p>
                <p class="member-bio">{{ businessDivision.bio }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Divisi Operasional -->
        <div class="division-section">
          <h3 class="division-title">Divisi Operasional</h3>
          <p class="division-description">
            Bertanggung jawab atas pelaksanaan operasional sehari-hari dan layanan kepada anggota
          </p>
          <div class="division-grid">
            <div 
              class="division-member"
              v-motion
              :initial="{ opacity: 0, y: 30 }"
              :enter="{ opacity: 1, y: 0 }"
              :delay="500"
            >
              <div class="member-image-container">
                <img 
                  :src="operationalDivision.image" 
                  :alt="operationalDivision.name"
                  class="member-image"
                  @error="handleImageError"
                />
                <div class="member-overlay">
                  <div class="member-name">{{ operationalDivision.name }}</div>
                  <div class="member-position">{{ operationalDivision.position }}</div>
                </div>
              </div>
              <div class="member-content">
                <h4 class="member-name-mobile">{{ operationalDivision.name }}</h4>
                <p class="member-position-mobile">{{ operationalDivision.position }}</p>
                <p class="member-bio">{{ operationalDivision.bio }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Divisi Keuangan -->
        <div class="division-section">
          <h3 class="division-title">Divisi Keuangan</h3>
          <p class="division-description">
            Mengelola keuangan koperasi, termasuk penghimpunan dana dan pembiayaan
          </p>
          <div class="division-grid">
            <div 
              class="division-member"
              v-motion
              :initial="{ opacity: 0, y: 30 }"
              :enter="{ opacity: 1, y: 0 }"
              :delay="600"
            >
              <div class="member-image-container">
                <img 
                  :src="financeDivision.image" 
                  :alt="financeDivision.name"
                  class="member-image"
                  @error="handleImageError"
                />
                <div class="member-overlay">
                  <div class="member-name">{{ financeDivision.name }}</div>
                  <div class="member-position">{{ financeDivision.position }}</div>
                </div>
              </div>
              <div class="member-content">
                <h4 class="member-name-mobile">{{ financeDivision.name }}</h4>
                <p class="member-position-mobile">{{ financeDivision.position }}</p>
                <p class="member-bio">{{ financeDivision.bio }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
interface Member {
  id: number
  name: string
  position: string
  bio: string
  image: string
  division: string
}

const businessDivision: Member = {
  id: 1,
  name: 'Tim Divisi Bisnis',
  position: 'Kepala Divisi',
  bio: 'Berfokus pada pengembangan produk dan ekspansi pasar',
  image: '/divisi/bisnis.png',
  division: 'bisnis'
}

const operationalDivision: Member = {
  id: 2,
  name: 'Tim Divisi Operasional',
  position: 'Kepala Divisi',
  bio: 'Mengawasi operasional harian dan layanan anggota',
  image: '/divisi/operasionalstaff.jpg',
  division: 'operasional'
}

const financeDivision: Member = {
  id: 3,
  name: 'Tim Divisi Keuangan',
  position: 'Kepala Divisi',
  bio: 'Mengelola portofolio pembiayaan dan pengembalian investasi',
  image: '/divisi/finance.jpg',
  division: 'keuangan'
}

const handleImageError = (event: Event) => {
  const target = event.target as HTMLImageElement;
  target.src = '/src/assets/default-avatar.png'; // Gambar fallback jika gambar tidak ditemukan
}
</script>

<style scoped>
.divisions {
  background: var(--gray-light);
  position: relative;
  overflow: hidden;
  padding: 4rem 0;
}

.divisions::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="dots" width="20" height="20" patternUnits="userSpaceOnUse"><circle cx="10" cy="10" r="1" fill="rgba(10,29,55,0.05)"/></pattern></defs><rect width="100" height="100" fill="url(%23dots)"/></svg>');
}

.divisions-content {
  position: relative;
  z-index: 2;
}

.divisions-header {
  text-align: center;
  margin-bottom: 4rem;
}

.divisions-header h2 {
  color: var(--primary-color);
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.divisions-header p {
  color: var(--gray-medium);
  font-size: 1.2rem;
}

.division-section {
  margin-bottom: 4rem;
}

.division-title {
  color: var(--primary-color);
  font-size: 1.8rem;
  font-weight: 600;
  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
  border-bottom: 3px solid var(--accent-color);
}

.division-description {
  color: var(--gray-medium);
  font-size: 1.1rem;
  margin-bottom: 2rem;
  text-align: center;
}

.division-grid {
  display: flex;
  justify-content: center;
  margin-bottom: 2rem;
}

.division-member {
  background: var(--white);
  border-radius: 16px;
  box-shadow: var(--shadow);
  overflow: hidden;
  transition: all 0.3s ease;
  position: relative;
  max-width: 600px;
  width: 100%;
}

.division-member:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-hover);
}

.member-image-container {
  position: relative;
  overflow: hidden;
  height: 300px;
}

.member-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.division-member:hover .member-image {
  transform: scale(1.05);
}

.member-overlay {
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

.division-member:hover .member-overlay {
  transform: translateY(0);
}

.member-name {
  font-size: 1.4rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.member-position {
  font-size: 1rem;
  color: #ddd;
}

.member-content {
  padding: 1.5rem;
  text-align: center;
}

.member-name-mobile {
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--primary-color);
  margin: 0 0 0.5rem 0;
  display: none;
}

.member-position-mobile {
  color: var(--accent-color);
  font-weight: 500;
  margin-bottom: 1rem;
  display: none;
}

.member-bio {
  color: var(--gray-medium);
  font-size: 0.95rem;
  line-height: 1.6;
}

@media (max-width: 768px) {
  .divisions-header h2 {
    font-size: 2rem;
  }
  
  .division-grid {
    grid-template-columns: 1fr;
  }
  
  .member-overlay {
    transform: translateY(0); /* Tampilkan info di mobile */
  }
  
  .member-name-mobile, 
  .member-position-mobile {
    display: block;
  }
  
  .member-overlay {
    display: none; /* Sembunyikan overlay di mobile karena info ditampilkan di bawah */
  }
}
</style>