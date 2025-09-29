<template>
  <section id="layanan" class="section services">
    <div class="container">
      <div 
        class="section-header"
        v-motion
        :initial="{ opacity: 0, y: 30 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="200"
      >
        <h2 class="section-title">Produk & Layanan</h2>
        <p class="section-subtitle">
          Berbagai produk dan layanan keuangan yang sesuai dengan kebutuhan Anda
        </p>
      </div>

      <div class="services-grid">
        <div 
          v-for="(service, index) in services"
          :key="service.id"
          class="service-card card"
          @click="selectedService = service"
        >
          <div class="service-icon" :style="{ backgroundColor: service.color }">
            {{ service.icon }}
          </div>
          <h3>{{ service.title }}</h3>
          <p>{{ service.description }}</p>
          <ul class="service-features">
            <li v-for="feature in service.features" :key="feature">{{ feature }}</li>
          </ul>
          <button class="btn btn-primary service-btn">Pelajari Selengkapnya</button>
        </div>
      </div>

      <!-- Modal untuk detail layanan -->
      <div v-if="selectedService" class="modal-overlay" @click="selectedService = null">
        <div class="modal-content" @click.stop>
          <button class="modal-close" @click="selectedService = null">&times;</button>
          <div class="modal-header">
            <div class="service-icon large" :style="{ backgroundColor: selectedService.color }">
              {{ selectedService.icon }}
            </div>
            <h3>{{ selectedService.title }}</h3>
          </div>
          <div class="modal-body">
            <p>{{ selectedService.fullDescription }}</p>
            <h4>Keunggulan:</h4>
            <ul>
              <li v-for="benefit in selectedService.benefits" :key="benefit">{{ benefit }}</li>
            </ul>
            <h4>Syarat & Ketentuan:</h4>
            <ul>
              <li v-for="requirement in selectedService.requirements" :key="requirement">{{ requirement }}</li>
            </ul>
          </div>
          <div class="modal-footer">
            <a href="#kontak" class="btn btn-primary" @click="selectedService = null">Hubungi Kami</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Service {
  id: number
  title: string
  description: string
  fullDescription: string
  icon: string
  color: string
  features: string[]
  benefits: string[]
  requirements: string[]
}

const selectedService = ref<Service | null>(null)

const services: Service[] = [
  {
    id: 1,
    title: 'Simpanan Berjangka',
    description: 'Simpanan dengan jangka waktu tertentu dan bunga yang menarik',
    fullDescription: 'Simpanan Berjangka adalah produk investasi jangka panjang dengan tingkat pengembalian yang kompetitif dan risiko yang minimal. Cocok untuk perencanaan keuangan masa depan.',
    icon: '💰',
    color: '#FFD700',
    features: ['Bunga kompetitif', 'Jangka waktu fleksibel', 'Aman dan terjamin'],
    benefits: [
      'Suku bunga hingga 8% per tahun',
      'Pilihan jangka waktu 6, 12, 24, dan 36 bulan',
      'Dapat dijadikan jaminan pinjaman',
      'Bebas biaya administrasi'
    ],
    requirements: [
      'Fotokopi KTP yang masih berlaku',
      'Setoran minimal Rp 1.000.000',
      'Mengisi formulir pembukaan rekening',
      'Menjadi anggota koperasi'
    ]
  },
  {
    id: 2,
    title: 'Pinjaman Usaha',
    description: 'Pinjaman untuk mengembangkan usaha dengan bunga rendah',
    fullDescription: 'Pinjaman Usaha dirancang khusus untuk membantu anggota mengembangkan dan memulai usaha dengan suku bunga yang kompetitif dan proses yang mudah.',
    icon: '🏢',
    color: '#4CAF50',
    features: ['Bunga rendah', 'Proses cepat', 'Tenor fleksibel'],
    benefits: [
      'Suku bunga mulai dari 12% per tahun',
      'Limit pinjaman hingga Rp 500.000.000',
      'Tenor hingga 60 bulan',
      'Proses persetujuan 3-7 hari kerja'
    ],
    requirements: [
      'Fotokopi KTP dan KK',
      'Surat keterangan usaha',
      'Laporan keuangan usaha 6 bulan terakhir',
      'Jaminan sesuai ketentuan'
    ]
  },
  {
    id: 3,
    title: 'Pembiayaan Pensiun',
    description: 'Solusi keuangan untuk persiapan masa pensiun yang nyaman',
    fullDescription: 'Program pembiayaan khusus untuk mempersiapkan masa pensiun yang nyaman dengan sistem pembayaran yang disesuaikan dengan kemampuan anggota.',
    icon: '👴',
    color: '#2196F3',
    features: ['Investasi jangka panjang', 'Manfaat pensiun', 'Fleksibel'],
    benefits: [
      'Manfaat pensiun bulanan tetap',
      'Asuransi jiwa gratis',
      'Dapat dicairkan kapan saja',
      'Tax benefit sesuai ketentuan'
    ],
    requirements: [
      'Usia minimal 21 tahun',
      'Fotokopi KTP dan slip gaji',
      'Setoran awal minimal Rp 500.000',
      'Iuran bulanan minimal Rp 100.000'
    ]
  },
  {
    id: 4,
    title: 'Layanan Digital',
    description: 'Akses mudah melalui aplikasi mobile dan internet banking',
    fullDescription: 'Layanan Digital memberikan kemudahan akses 24/7 untuk melakukan berbagai transaksi keuangan melalui aplikasi mobile dan internet banking yang user-friendly.',
    icon: '📱',
    color: '#9C27B0',
    features: ['24/7 akses', 'Transfer online', 'Monitoring real-time'],
    benefits: [
      'Transaksi kapan saja, dimana saja',
      'Cek saldo dan mutasi real-time',
      'Transfer antar bank',
      'Pembayaran tagihan lengkap'
    ],
    requirements: [
      'Memiliki rekening di koperasi',
      'Smartphone dengan koneksi internet',
      'Email aktif untuk verifikasi',
      'Nomor HP aktif untuk SMS OTP'
    ]
  }
]
</script>

<style scoped>
.services {
  background: var(--white);
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.service-card {
  text-align: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.service-card:hover {
  transform: translateY(-10px);
}

.service-icon {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  margin: 0 auto 1.5rem;
  color: var(--primary-color);
}

.service-icon.large {
  width: 100px;
  height: 100px;
  font-size: 2.5rem;
}

.service-card h3 {
  color: var(--primary-color);
  font-size: 1.4rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.service-card p {
  color: var(--gray-medium);
  margin-bottom: 1.5rem;
}

.service-features {
  list-style: none;
  margin-bottom: 2rem;
}

.service-features li {
  color: var(--gray-medium);
  padding: 0.5rem 0;
  border-bottom: 1px solid #E9ECEF;
}

.service-features li:last-child {
  border-bottom: none;
}

.service-btn {
  width: 100%;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  padding: 1rem;
}

.modal-content {
  background: var(--white);
  border-radius: 16px;
  max-width: 600px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
}

.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: var(--gray-medium);
  z-index: 1;
}

.modal-close:hover {
  color: var(--primary-color);
}

.modal-header {
  text-align: center;
  padding: 2rem 2rem 1rem;
}

.modal-header h3 {
  color: var(--primary-color);
  font-size: 1.5rem;
  font-weight: 600;
  margin-top: 1rem;
}

.modal-body {
  padding: 0 2rem 1rem;
}

.modal-body p {
  color: var(--gray-medium);
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.modal-body h4 {
  color: var(--primary-color);
  font-weight: 600;
  margin: 1.5rem 0 0.5rem;
}

.modal-body ul {
  color: var(--gray-medium);
  padding-left: 1.5rem;
}

.modal-body li {
  margin-bottom: 0.5rem;
}

.modal-footer {
  padding: 1rem 2rem 2rem;
  text-align: center;
}

@media (max-width: 768px) {
  .services-grid {
    grid-template-columns: 1fr;
  }
  
  .modal-content {
    margin: 1rem;
    max-height: 85vh;
  }
}
</style>