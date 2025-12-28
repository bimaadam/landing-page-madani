<template>
  <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
    <div class="container">
      <div class="navbar-content">
        <!-- Brand -->
        <div class="navbar-brand">
          <img src="/logo.png" alt="Koperasi Athaya Raya Madani Logo" class="logo">
          <div class="brand-text-container">
            <span class="brand-text">KOPERASI ATHAYA RAYA MADANI</span>
            <span class="brand-subtext">KOPERASI SIMPAN PINJAM</span>
          </div>
        </div>

        <!-- Menu -->
        <div class="navbar-menu" :class="{ 'navbar-menu-open': isMenuOpen }">
          <a href="#beranda" class="navbar-link" @click="closeMenu">Beranda</a>

          <div class="navbar-dropdown" @mouseenter="showSubmenu = true" @mouseleave="showSubmenu = false">
            <button class="navbar-link dropdown-button" @click="toggleSubmenu">
              Tentang Kami
              <i class="bi bi-chevron-down dropdown-icon" :class="{ 'rotate-icon': showSubmenu }"></i>
            </button>

            <div class="dropdown-menu" :class="{ 'show': showSubmenu }">
              <a href="#tentang" class="dropdown-link" @click="closeMenu">Sejarah Koperasi ARM</a>
              <a href="#pengurus" class="dropdown-link" @click="closeMenu">Pengurus</a>
              <a href="#about-section" class="dropdown-link" @click="closeMenu">Visi & Misi</a>
            </div>
          </div>

          <a href="#layanan" class="navbar-link" @click="closeMenu">Produk & Layanan</a>
          
          <a href="https://athayarayamadani.co.id/kreditpensiun/auth/login" 
             target="_blank" 
             rel="noopener noreferrer"
             class="navbar-link navbar-link-special" 
             @click="closeMenu">
            Aplikasi Kresun
          </a>

          <a href="#kontak" class="navbar-link" @click="closeMenu">Kontak</a>
        </div>

        <!-- Mobile Toggle -->
        <button class="navbar-toggle" 
                @click="toggleMenu" 
                :class="{ 'navbar-toggle-open': isMenuOpen }"
                aria-label="Toggle menu">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMenuOpen = ref(false)
const showSubmenu = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const toggleSubmenu = () => {
  showSubmenu.value = !showSubmenu.value
}

const closeMenu = () => {
  isMenuOpen.value = false
  showSubmenu.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  
  document.addEventListener('click', (event) => {
    const target = event.target
    if (!target.closest('.navbar-dropdown')) {
      showSubmenu.value = false
    }
  })
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
  background: rgba(10, 29, 55, 0.85);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  z-index: 1000;
  transition: all 0.3s ease;
}

.navbar-scrolled {
  background: rgba(10, 29, 55, 0.95);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.navbar-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
}

/* Brand */
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
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--accent-color);
  line-height: 1.2;
}

.brand-subtext {
  font-size: 0.75rem;
  font-weight: 500;
  color: var(--white);
  opacity: 0.9;
}

/* Menu */
.navbar-menu {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}

.navbar-link {
  color: var(--white);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.95rem;
  padding: 8px 16px;
  border-radius: 6px;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 6px;
  white-space: nowrap;
}

.navbar-link:hover {
  background-color: var(--accent-color);
  color: var(--primary-color);
}

.navbar-link-special {
  background-color: var(--accent-color);
  color: var(--primary-color);
  font-weight: 600;
}

.navbar-link-special:hover {
  background-color: #FFC700;
  transform: translateY(-2px);
}

/* Dropdown */
.navbar-dropdown {
  position: relative;
}

.dropdown-button {
  cursor: pointer;
  background: none;
  border: none;
  font-family: inherit;
  font-size: 0.95rem;
}

.dropdown-icon {
  font-size: 0.75rem;
  transition: transform 0.3s ease;
}

.rotate-icon {
  transform: rotate(180deg);
}

.dropdown-menu {
  position: absolute;
  top: calc(100% + 8px);
  left: 0;
  background: var(--primary-color);
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  min-width: 220px;
  opacity: 0;
  visibility: hidden;
  transform: translateY(-10px);
  transition: all 0.3s ease;
  overflow: hidden;
}

.dropdown-menu.show {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.dropdown-link {
  display: block;
  padding: 12px 20px;
  color: var(--white);
  text-decoration: none;
  font-size: 0.9rem;
  transition: all 0.3s ease;
}

.dropdown-link:hover {
  background-color: var(--accent-color);
  color: var(--primary-color);
  padding-left: 24px;
}

/* Mobile Toggle */
.navbar-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.navbar-toggle span {
  width: 28px;
  height: 3px;
  background-color: var(--white);
  border-radius: 2px;
  transition: all 0.3s ease;
}

.navbar-toggle-open span:nth-child(1) {
  transform: rotate(45deg) translate(7px, 7px);
}

.navbar-toggle-open span:nth-child(2) {
  opacity: 0;
}

.navbar-toggle-open span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -7px);
}

/* Responsive */
@media (max-width: 768px) {
  .brand-text {
    font-size: 0.9rem;
  }

  .brand-subtext {
    font-size: 0.65rem;
  }

  .logo {
    width: 40px;
    height: 40px;
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
    gap: 0;
    padding: 1rem 0;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  }

  .navbar-menu-open {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }

  .navbar-link {
    width: 100%;
    padding: 12px 1.5rem;
    border-radius: 0;
  }

  .dropdown-menu {
    position: static;
    transform: none;
    box-shadow: none;
    background: rgba(0, 0, 0, 0.2);
    margin: 0;
  }

  .dropdown-menu.show {
    transform: none;
  }

  .dropdown-link {
    padding-left: 2.5rem;
  }

  .dropdown-link:hover {
    padding-left: 3rem;
  }
}
</style>