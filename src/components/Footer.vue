<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section company">
          <div class="footer-brand">
            <img src="/logo.png" alt="Logo" class="footer-logo">
            <h3>Koperasi Athaya Raya Madani</h3>
          </div>
          <p class="company-description">
            Koperasi terpercaya yang melayani simpan pinjam dan pembiayaan syariah 
            untuk kesejahteraan anggota dan masyarakat Bandung sejak 2022.
          </p>
          <div class="company-certifications">
            <span class="cert-badge">Terdaftar OJK</span>
            <span class="cert-badge">ISO 9001:2022</span>
          </div>
        </div>

        <div class="footer-section links">
          <h4>Navigasi</h4>
          <ul>
            <li><a href="#beranda">Beranda</a></li>
            <li><a href="#tentang">Tentang Kami</a></li>
            <li><a href="#layanan">Produk & Layanan</a></li>
            <li><a href="#testimoni">Testimoni</a></li>
            <li><a href="#kontak">Kontak</a></li>
          </ul>
        </div>

        <div class="footer-section services">
          <h4>Layanan</h4>
          <ul>
            <li><a href="#layanan">Simpanan Berjangka</a></li>
            <li><a href="#layanan">Pinjaman Usaha</a></li>
            <li><a href="#layanan">Pembiayaan Pensiun</a></li>
            <li><a href="#layanan">Layanan Digital</a></li>
            <li><a href="#kontak">Konsultasi Gratis</a></li>
          </ul>
        </div>

        <div class="footer-section contact">
          <h4>Kontak Kami</h4>
          <div class="contact-info">
            <div class="contact-item">
              <span class="contact-icon">📍</span>
              <span>Jl. Venus Bar., Manjahlega, Kec. Rancasari, Kota Bandung, Jawa Barat 40286</span>
            </div>
            <div class="contact-item">
              <span class="contact-icon">📞</span>
              <span>
                <a href="tel:+622212345678">(022) 1234-5678</a><br>
                <a href="https://wa.me/6281234567890">+62 812-3456-7890</a>
              </span>
            </div>
            <div class="contact-item">
              <span class="contact-icon">✉️</span>
              <span><a href="mailto:info@athayarayamadani.com">info@athayarayamadani.com</a></span>
            </div>
            <div class="contact-item">
              <span class="contact-icon">🕒</span>
              <span>Sen-Jum: 08:00-17:00 WIB<br>Sabtu: 08:00-15:00 WIB</span>
            </div>
          </div>
        </div>

        <div class="footer-section maps">
          <h4>Lokasi Kami</h4>
          <MapsEmbed />
        </div>

        <div class="footer-section newsletter">
          <h4>Newsletter</h4>
          <p>Dapatkan info terbaru seputar produk dan promosi menarik</p>
          <form @submit.prevent="subscribeNewsletter" class="newsletter-form">
            <div class="newsletter-input">
              <input 
                type="email" 
                v-model="newsletterEmail" 
                placeholder="Masukkan email Anda"
                required
              >
              <button type="submit" :disabled="isSubscribing">
                <span v-if="!isSubscribing">Daftar</span>
                <span v-else>...</span>
              </button>
            </div>
          </form>
          
          <div class="social-media">
            <h5>Ikuti Kami</h5>
            <div class="social-links">
              <a href="#" class="social-link facebook" title="Facebook">📘</a>
              <a href="#" class="social-link instagram" title="Instagram">📸</a>
              <a href="#" class="social-link youtube" title="YouTube">📺</a>
              <a href="#" class="social-link linkedin" title="LinkedIn">💼</a>
              <a href="#" class="social-link twitter" title="Twitter">🐦</a>
            </div>
          </div>
        </div>
      </div>
      </div>

      <div class="footer-bottom">
        <div class="footer-bottom-content">
          <div class="copyright">
            <p>&copy; 2025 Koperasi Athaya Raya Madani Bandung. All rights reserved.</p>
          </div>
          
          <div class="footer-bottom-links">
            <a href="#">Syarat & Ketentuan</a>
            <a href="#">Kebijakan Privasi</a>
            <a href="#">FAQ</a>
            <a href="#">Sitemap</a>
          </div>
          
          <div class="footer-bottom-info">
            <p>Badan Hukum: No. 518.2/123/BH/KWK.11/X/2022</p>
          </div>
        </div>
      </div>
  </footer>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import MapsEmbed from './MapsEmbed.vue'

const newsletterEmail = ref('')
const isSubscribing = ref(false)

const subscribeNewsletter = async () => {
  isSubscribing.value = true
  
  // Simulate API call
  try {
    await new Promise(resolve => setTimeout(resolve, 1000))
    alert('Terima kasih! Anda telah berhasil berlangganan newsletter.')
    newsletterEmail.value = ''
  } catch (error) {
    alert('Terjadi kesalahan. Silakan coba lagi.')
  } finally {
    isSubscribing.value = false
  }
}
</script>

<style scoped>
.footer {
  background: var(--primary-color);
  color: var(--white);
  padding: 60px 0 0;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr 1.5fr;
  gap: 2rem;
  margin-bottom: 3rem;
}

/* Menyesuaikan urutan section di footer */
.footer-section.maps {
  grid-column: 1 / span 2; /* Peta menempati 2 kolom */
}

.footer-section h4, .footer-section h5 {
  color: var(--accent-color);
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 1.5rem;
}

.footer-section h5 {
  font-size: 1rem;
  margin-top: 2rem;
  margin-bottom: 1rem;
}

/* Company Section */
.footer-brand {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 1rem;
}

.footer-logo {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  object-fit: cover;
}

.footer-brand h3 {
  color: var(--white);
  font-size: 1.3rem;
  font-weight: 600;
  margin: 0;
}

.company-description {
  line-height: 1.6;
  margin-bottom: 1.5rem;
  opacity: 0.9;
}

.company-certifications {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.cert-badge {
  background: var(--accent-color);
  color: var(--primary-color);
  font-size: 0.8rem;
  font-weight: 600;
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
}

/* Links Section */
.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section li {
  margin-bottom: 0.75rem;
}

.footer-section a {
  color: var(--white);
  text-decoration: none;
  opacity: 0.8;
  transition: all 0.3s ease;
}

.footer-section a:hover {
  opacity: 1;
  color: var(--accent-color);
}

/* Contact Section */
.contact-info {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
}

.contact-icon {
  font-size: 1.2rem;
  flex-shrink: 0;
  opacity: 0.8;
}

.contact-item span:last-child {
  line-height: 1.4;
}

.address-link {
  color: var(--white);
  text-decoration: none;
  transition: all 0.3s ease;
}

.address-link:hover {
  color: var(--accent-color);
  text-decoration: underline;
}

/* Newsletter Section */
.newsletter p {
  opacity: 0.9;
  margin-bottom: 1.5rem;
  line-height: 1.5;
}

.newsletter-form {
  margin-bottom: 2rem;
}

.newsletter-input {
  display: flex;
  background: var(--white);
  border-radius: 6px;
  overflow: hidden;
}

.newsletter-input input {
  flex: 1;
  padding: 12px;
  border: none;
  font-family: inherit;
  outline: none;
}

.newsletter-input button {
  background: var(--accent-color);
  color: var(--primary-color);
  border: none;
  padding: 12px 20px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease;
}

.newsletter-input button:hover:not(:disabled) {
  background: #E6C200;
}

.newsletter-input button:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

/* Social Media */
.social-links {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 45px;
  height: 45px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  font-size: 1.2rem;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-link:hover {
  background: var(--accent-color);
  transform: translateY(-2px);
}

/* Footer Bottom */
.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding: 2rem 0;
}

.footer-bottom-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 2rem;
  flex-wrap: wrap;
}

.copyright p {
  margin: 0;
  opacity: 0.8;
}

.footer-bottom-links {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.footer-bottom-links a {
  color: var(--white);
  text-decoration: none;
  opacity: 0.8;
  font-size: 0.9rem;
  transition: opacity 0.3s ease;
}

.footer-bottom-links a:hover {
  opacity: 1;
}

.footer-bottom-info p {
  margin: 0;
  opacity: 0.7;
  font-size: 0.9rem;
}

@media (max-width: 1024px) {
  .footer-content {
    grid-template-columns: 1fr 1fr 1fr 1fr;
    gap: 1.5rem;
  }
  
  .footer-section.company {
    grid-column: span 4;
  }
  
  .footer-section.maps {
    grid-column: span 2;
  }
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .footer-section.company {
    grid-column: span 1;
  }
  
  .footer-section.maps {
    grid-column: span 1;
  }
  
  .footer-brand {
    flex-direction: column;
    text-align: center;
    gap: 1rem;
  }
  
  .company-certifications {
    justify-content: center;
  }
  
  .footer-bottom-content {
    flex-direction: column;
    text-align: center;
  }
  
  .footer-bottom-links {
    justify-content: center;
  }
  
  .social-links {
    justify-content: center;
  }
}
</style>