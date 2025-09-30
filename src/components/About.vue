<template>
  <section id="tentang" class="section about">
    <div class="container">
      <div 
        class="section-header"
        v-motion
        :initial="{ opacity: 0, y: 30 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="200"
      >
        <h2 class="section-title">Tentang Kami</h2>
        <p class="section-subtitle">
          Mengenal lebih dekat Koperasi Athaya Raya Madani Bandung, sejarah.
        </p>
      </div>

      <div class="about-content">
        <div 
          class="about-text"
          v-motion
          :initial="{ opacity: 0, x: -50 }"
          :enter="{ opacity: 1, x: 0 }"
          :delay="300"
        >
          <div class="about-section">
            <h3>Sejarah Singkat</h3>
            <p>
               Koperasi Athaya Raya Madani didirikan pada 7 Februari 2022 sebagai Koperasi Simpan Pinjam berbentuk Koperasi Primer Nasional yang berlokasi di Kota Bandung, Jawa Barat.
Kami menyediakan layanan pinjaman pensiun untuk ASN/PNS, TNI, Polri, serta pinjaman konsumer lainnya, dengan dukungan Service Level Agreement (SLA) yang cepat dan efisien.
Jaringan layanan kami telah tersebar di wilayah Sumatera, Jawa, Bali, dan Nusa Tenggara Barat-Timur.
Kami menjunjung tinggi integritas dan selalu menempatkan pelayanan anggota dan masyarakat sebagai prioritas. Komitmen kami adalah membangun koperasi yang terdepan, modern, dan terpercaya.
Dengan semangat kolaborasi dan inovasi, kami yakin Koperasi Athaya Raya Madani akan terus tumbuh menjadi koperasi unggulan di seluruh Indonesia. 
            </p>
          </div>

          <div class="about-section">
            <h3>Visi</h3>
            <p>
              Terwujudnya Koperasi yang mandiri dan unggul, serta meningkatakan kesejahteraan Anggota dan masyarakat
            </p>
          </div>

          <div class="about-section">
            <h3>Misi</h3>
            <ul>
              <li>Mewujudkan Koperasi yang profesional, akuntabilitas dan transparan</li>
              <li>Mengembangkan Koperasi dan kerjasama Kemitraan</li>
              <li>Menumbuh kembangkan diverifikasi produk simpan pinjam dan pelayanan Koperasi untuk Anggota</li>
            </ul>
          </div>
        </div>

        <div 
          class="about-visual"
          v-motion
          :initial="{ opacity: 0, x: 50 }"
          :enter="{ opacity: 1, x: 0 }"
          :delay="400"
        >
          <div class="visual-card">
            <img src="https://images.pexels.com/photos/3184298/pexels-photo-3184298.jpeg?auto=compress&cs=tinysrgb&w=600" alt="Kantor Koperasi" />
            <div class="visual-overlay">
              <div class="visual-content">
                <h4>Kantor Pusat Bandung</h4>
                <p>Lokasi strategis di jantung kota Bandung</p>
              </div>
            </div>
          </div>

          <!-- <div class="certifications">
            <h4>Legalitas & Sertifikasi</h4>
            <div class="cert-grid">
              <div class="cert-item">
                <div class="cert-icon">📋</div>
                <div class="cert-info">
                  <h5>Badan Hukum Koperasi</h5>
                  <p>No. 518.2/123/BH/KWK.11/X/2015</p>
                </div>
              </div>
              
              <div class="cert-item">
                <div class="cert-icon">🏛️</div>
                <div class="cert-info">
                  <h5>Izin Usaha Koperasi</h5>
                  <p>Dinas Koperasi Jawa Barat</p>
                </div>
              </div>
              
              <div class="cert-item">
                <div class="cert-icon">🛡️</div>
                <div class="cert-info">
                  <h5>Sertifikat ISO 9001:2015</h5>
                  <p>Manajemen Mutu Terjamin</p>
                </div>
              </div>
            </div>
          </div> -->
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
// No additional script needed
</script>

<style scoped>
.about {
  background: var(--gray-light);
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

.about-section {
  margin-bottom: 2.5rem;
}

.about-section h3 {
  color: var(--primary-color);
  font-size: 1.4rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.about-section p, .about-section li {
  color: var(--gray-medium);
  line-height: 1.7;
}

.about-section ul {
  padding-left: 1.5rem;
}

.about-section li {
  margin-bottom: 0.5rem;
}

.visual-card {
  position: relative;
  border-radius: 16px;
  overflow: hidden;
  margin-bottom: 2rem;
  box-shadow: var(--shadow);
}

.visual-card img {
  width: 100%;
  height: 300px;
  object-fit: cover;
}

.visual-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(10, 29, 55, 0.8));
  padding: 2rem;
  color: var(--white);
}

.visual-content h4 {
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.certifications {
  background: var(--white);
  padding: 2rem;
  border-radius: 12px;
  box-shadow: var(--shadow);
}

.certifications h4 {
  color: var(--primary-color);
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 1.5rem;
}

.cert-grid {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.cert-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.cert-icon {
  font-size: 1.5rem;
  flex-shrink: 0;
}

.cert-info h5 {
  color: var(--primary-color);
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.cert-info p {
  color: var(--gray-medium);
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  .about-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
}
</style>