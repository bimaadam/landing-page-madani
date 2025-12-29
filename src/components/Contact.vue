<template>
  <section id="kontak" class="section contact">
    <div class="container">
      <div 
        class="section-header"
        v-motion
        :initial="{ opacity: 0, y: 30 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="200"
      >
        <h2 class="section-title">Hubungi Kami</h2>
        <p class="section-subtitle">
          Siap melayani Anda dengan sepenuh hati. Hubungi kami untuk konsultasi atau bergabung menjadi anggota
        </p>
      </div>

      <div class="contact-content">
        <div 
          class="contact-info"
          v-motion
          :initial="{ opacity: 0, x: -50 }"
          :enter="{ opacity: 1, x: 0 }"
          :delay="300"
        >
          <div class="info-card">
            <h3>Informasi Kontak</h3>
            
            <div class="info-item">
              <i class="bi bi-geo-alt-fill info-icon"></i>
              <div class="info-content">
                <h4>Alamat Kantor Pusat</h4>
                <p>JI. Cipamokolan No.8 RT.003 RW.001 Kel. Cipamokolan Kec. Rancasari<br>Kota Bandung 40292</p>
              </div>
            </div>

            <div class="info-item">
              <i class="bi bi-telephone-fill info-icon"></i>
              <div class="info-content">
                <h4>Telepon</h4>
                <p>
                  <a href="tel:+622287516947">022-87516947</a><br>
                  <!-- <a href="https://wa.me/022-87516947" target="_blank">+62 812</a> -->
                </p>
              </div>
            </div>

            <div class="info-item">
              <i class="bi bi-envelope-fill info-icon"></i>
              <div class="info-content">
                <h4>Email</h4>
                <p>
                  <a href="https://www.athayarayamadani.co.id">https://www.athayarayamadani.co.id</a><br>
                  <a href="mailto:arm.koperasi@athayarayamadani.co.id">arm.koperasi@athayarayamadani.co.id</a>
                </p>
              </div>
            </div>

            <div class="info-item">
              <i class="bi bi-clock-fill info-icon"></i>
              <div class="info-content">
                <h4>Jam Operasional</h4>
                <p>
                  Senin - Jumat: 08:00 - 17:00 WIB<br>
                  Sabtu: 08:00 - 15:00 WIB<br>
                  Minggu: Tutup
                </p>
              </div>
            </div>

            <div class="social-media">
              <h4>Ikuti Kami</h4>
              <div class="social-links">
                <a href="#" class="social-link facebook">
                  <i class="bi bi-facebook"></i>
                </a>
                <a href="#" class="social-link instagram">
                  <i class="bi bi-instagram"></i>
                </a>
                <a href="#" class="social-link youtube">
                  <i class="bi bi-youtube"></i>
                </a>
                <a href="#" class="social-link linkedin">
                  <i class="bi bi-linkedin"></i>
                </a>
              </div>
            </div>
          </div>
        </div>

        <div 
          class="contact-form-section"
          v-motion
          :initial="{ opacity: 0, x: 50 }"
          :enter="{ opacity: 1, x: 0 }"
          :delay="400"
        >
          <div class="form-card">
            <h3>Formulir Pendaftaran Online</h3>
            <p class="form-description">
              Isi formulir berikut untuk mendaftar sebagai anggota atau konsultasi layanan
            </p>

            <form @submit.prevent="submitForm" class="contact-form">
              <div class="form-row">
                <div class="form-group">
                  <label for="fullName" class="form-label">Nama Lengkap *</label>
                  <input 
                    type="text" 
                    id="fullName" 
                    v-model="form.fullName" 
                    class="form-control" 
                    required
                    placeholder="Masukkan nama lengkap"
                  >
                </div>

                <div class="form-group">
                  <label for="phone" class="form-label">Nomor Telepon *</label>
                  <input 
                    type="tel" 
                    id="phone" 
                    v-model="form.phone" 
                    class="form-control" 
                    required
                    placeholder="08xx-xxxx-xxxx"
                  >
                </div>
              </div>

              <div class="form-row">
                <div class="form-group">
                  <label for="email" class="form-label">Email *</label>
                  <input 
                    type="email" 
                    id="email" 
                    v-model="form.email" 
                    class="form-control" 
                    required
                    placeholder="nama@email.com"
                  >
                </div>

                <div class="form-group">
                  <label for="profession" class="form-label">Pekerjaan</label>
                  <input 
                    type="text" 
                    id="profession" 
                    v-model="form.profession" 
                    class="form-control"
                    placeholder="Pekerjaan Anda"
                  >
                </div>
              </div>

              <div class="form-group">
                <label for="address" class="form-label">Alamat *</label>
                <textarea 
                  id="address" 
                  v-model="form.address" 
                  class="form-control" 
                  rows="3" 
                  required
                  placeholder="Alamat lengkap Anda"
                ></textarea>
              </div>

              <div class="form-group">
                <label for="service" class="form-label">Layanan yang Diminati *</label>
                <select id="service" v-model="form.service" class="form-control" required>
                  <option value="">Pilih layanan</option>
                  <option value="simpanan">Simpanan Berjangka</option>
                  <option value="pinjaman">Pinjaman Usaha</option>
                  <option value="pensiun">Pembiayaan Pensiun</option>
                  <option value="digital">Layanan Digital</option>
                  <option value="konsultasi">Konsultasi</option>
                </select>
              </div>

              <div class="form-group">
                <label for="message" class="form-label">Pesan / Pertanyaan</label>
                <textarea 
                  id="message" 
                  v-model="form.message" 
                  class="form-control" 
                  rows="4"
                  placeholder="Sampaikan pesan atau pertanyaan Anda"
                ></textarea>
              </div>

              <div class="form-group checkbox-group">
                <label class="checkbox-label">
                  <input type="checkbox" v-model="form.agreement" required>
                  <span class="checkmark"></span>
                  Saya setuju dengan <a href="#" class="link">Syarat & Ketentuan</a> dan <a href="#" class="link">Kebijakan Privasi</a>
                </label>
              </div>

              <button 
                type="submit" 
                class="btn btn-primary submit-btn" 
                :disabled="isSubmitting"
                :class="{ 'submitting': isSubmitting }"
              >
                <span v-if="!isSubmitting">{{ submitButtonText }}</span>
                <span v-else>Mengirim...</span>
              </button>
            </form>
          </div>
        </div>
      </div>

      <!-- Success Message -->
      <div v-if="showSuccess" class="success-message" v-motion-fade>
        <div class="success-content">
          <div class="success-icon">
            <i class="bi bi-check-circle-fill" style="color: #4CAF50; font-size: 4rem;"></i>
          </div>
          <h3>Formulir Berhasil Dikirim!</h3>
          <p>Terima kasih atas minat Anda. Tim kami akan menghubungi Anda dalam 1x24 jam.</p>
          <button @click="closeSuccess" class="btn btn-primary">Tutup</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'

interface FormData {
  fullName: string
  phone: string
  email: string
  profession: string
  address: string
  service: string
  message: string
  agreement: boolean
}

const form = reactive<FormData>({
  fullName: '',
  phone: '',
  email: '',
  profession: '',
  address: '',
  service: '',
  message: '',
  agreement: false
})

const isSubmitting = ref(false)
const showSuccess = ref(false)
const submitButtonText = ref('Daftar Sekarang')

const submitForm = async () => {
  isSubmitting.value = true
  
  // Simulate API call
  try {
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Reset form
    Object.keys(form).forEach(key => {
      if (typeof form[key as keyof FormData] === 'boolean') {
        form[key as keyof FormData] = false as any
      } else {
        form[key as keyof FormData] = '' as any
      }
    })
    
    showSuccess.value = true
  } catch (error) {
    console.error('Error submitting form:', error)
  } finally {
    isSubmitting.value = false
  }
}

const closeSuccess = () => {
  showSuccess.value = false
}
</script>

<style scoped>
.contact {
  background: var(--white);
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 4rem;
  align-items: start;
}

.info-card, .form-card {
  background: var(--white);
  padding: 3rem;
  border-radius: 16px;
  box-shadow: var(--shadow);
  border: 1px solid #E9ECEF;
}

.info-card h3, .form-card h3 {
  color: var(--primary-color);
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 2rem;
}

.info-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 2rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid var(--gray-light);
}

.info-item:last-of-type {
  border-bottom: none;
  margin-bottom: 2rem;
}

.info-icon {
  font-size: 1.5rem;
  flex-shrink: 0;
  background: var(--gray-light);
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--accent-color);
}

.info-content h4 {
  color: var(--primary-color);
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.info-content p, .info-content a {
  color: var(--gray-medium);
  line-height: 1.5;
}

.info-content a {
  text-decoration: none;
  transition: color 0.3s ease;
}

.info-content a:hover {
  color: var(--accent-color);
}

.social-media h4 {
  color: var(--primary-color);
  font-weight: 600;
  margin-bottom: 1rem;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  font-size: 1.3rem;
  text-decoration: none;
  transition: all 0.3s ease;
  background: var(--gray-light);
  color: var(--primary-color);
}

.social-link:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow);
  background: var(--accent-color);
}

.form-description {
  color: var(--gray-medium);
  margin-bottom: 2rem;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.checkbox-group {
  margin-top: 1rem;
}

.checkbox-label {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  cursor: pointer;
  line-height: 1.5;
}

.checkbox-label input[type="checkbox"] {
  display: none;
}

.checkmark {
  width: 20px;
  height: 20px;
  border: 2px solid var(--gray-medium);
  border-radius: 4px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.checkbox-label input[type="checkbox"]:checked + .checkmark {
  background: var(--accent-color);
  border-color: var(--accent-color);
}

.checkbox-label input[type="checkbox"]:checked + .checkmark::after {
  content: '✓';
  color: var(--primary-color);
  font-weight: bold;
}

.link {
  color: var(--accent-color);
  text-decoration: none;
}

.link:hover {
  text-decoration: underline;
}

.submit-btn {
  width: 100%;
  padding: 15px;
  font-size: 1.1rem;
  font-weight: 600;
  transition: all 0.3s ease;
}

.submit-btn.submitting {
  opacity: 0.7;
  cursor: not-allowed;
}

.success-message {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 3000;
  padding: 1rem;
}

.success-content {
  background: var(--white);
  padding: 3rem;
  border-radius: 16px;
  text-align: center;
  max-width: 500px;
  width: 100%;
}

.success-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
}

.success-content h3 {
  color: var(--primary-color);
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.success-content p {
  color: var(--gray-medium);
  margin-bottom: 2rem;
}

@media (max-width: 768px) {
  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .info-card, .form-card {
    padding: 2rem;
  }
  
  .form-row {
    grid-template-columns: 1fr;
  }
  
  .social-links {
    justify-content: center;
  }
}
</style>