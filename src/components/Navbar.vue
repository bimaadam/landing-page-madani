<template>
  <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
    <div class="container">
      <div class="navbar-content">
        <div class="navbar-brand">
          <img src="/logo.png" alt="Logo" class="logo">
          <div class="brand-text-container">
            <span class="brand-text">KOPERASI ATHAYA RAYA MADANI</span>
            <span class="brand-subtext">KOPERASI SIMPAN PINJAM</span>
          </div>
        </div>
        
        <div class="navbar-menu" :class="{ 'navbar-menu-open': isMenuOpen }">
          <a href="#beranda" class="navbar-link" @click="closeMenu">Beranda</a>
          <a href="#tentang" class="navbar-link" @click="closeMenu">Tentang Kami</a>
          <a href="#layanan" class="navbar-link" @click="closeMenu">Produk & Layanan</a>
          <a href="#simpan-pinjam" class="navbar-link" @click="closeMenu">Simpan Pinjam</a>
          <a href="#kontak" class="navbar-link" @click="closeMenu">Kontak</a>
        </div>
        
        <button class="navbar-toggle" @click="toggleMenu" :class="{ 'navbar-toggle-open': isMenuOpen }">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMenuOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background: rgba(10, 29, 55, 0.11); /* fallback */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  z-index: 1000;
  transition: all 0.3s ease;
}


.navbar-scrolled {
  background: rgba(10, 29, 55, 0.9); /* Gunakan warna dasar dengan opacity */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  box-shadow: var(--shadow);
}

.navbar-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
}

.navbar-brand {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  object-fit: cover;
}

.brand-text-container {
  display: flex;
  flex-direction: column;
}

.brand-text {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--accent-color);
  margin-bottom: 2px;
}

.brand-subtext {
  font-size: 0.8rem;
  font-weight: 400;
  color: var(--white);
  opacity: 0.8;
}

.navbar-menu {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.navbar-link {
  color: var(--white);
  text-decoration: none;
  font-weight: 500;
  padding: 8px 16px;
  border-radius: 6px;
  transition: all 0.3s ease;
}

.navbar-link:hover {
  background-color: var(--accent-color);
  color: var(--primary-color);
}

.navbar-toggle {
  display: none;
  flex-direction: column;
  gap: 4px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.navbar-toggle span {
  width: 25px;
  height: 3px;
  background-color: var(--white);
  transition: all 0.3s ease;
}

.navbar-toggle-open span:nth-child(1) {
  transform: rotate(45deg) translate(6px, 6px);
}

.navbar-toggle-open span:nth-child(2) {
  opacity: 0;
}

.navbar-toggle-open span:nth-child(3) {
  transform: rotate(-45deg) translate(6px, -6px);
}

@media (max-width: 768px) {
  .brand-text {
    font-size: 1rem;
  }
  
  .brand-subtext {
    font-size: 0.7rem;
  }
  
  .navbar-toggle {
    display: flex;
  }
  
  .navbar-menu {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: var(--primary-color);
    flex-direction: column;
    padding: 2rem;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
  }
  
  .navbar-menu-open {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }
}
</style>