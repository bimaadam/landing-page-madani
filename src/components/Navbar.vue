<template>
  <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }" role="navigation" aria-label="Main navigation">
    <div class="container">
      <div class="navbar-content">
        <div class="navbar-brand">
          <img src="/logo.png" alt="Koperasi Athaya Raya Madani Logo" class="logo">
          <div class="brand-text-container">
            <span class="brand-text">KOPERASI ATHAYA RAYA MADANI</span>
            <span class="brand-subtext">KOPERASI SIMPAN PINJAM</span>
          </div>
        </div>

        <div class="navbar-menu" :class="{ 'navbar-menu-open': isMenuOpen }">
          <a href="#beranda" class="navbar-link" @click="closeMenu" @focus="onLinkFocus">Beranda</a>

          <div class="navbar-dropdown" @mouseenter="showSubmenu = true" @mouseleave="showSubmenu = false">
            <button type="button" class="navbar-link dropdown-button" @click="toggleSubmenu"
              @keydown.enter="toggleSubmenu" @keydown.space="toggleSubmenu" @keydown.escape="closeMenu"
              aria-haspopup="true" :aria-expanded="showSubmenu ? 'true' : 'false'"
              :aria-controls="'dropdown-menu-' + dropdownId">
              Tentang Kami
              <svg :class="{ 'rotate-icon': showSubmenu }" class="dropdown-icon" width="12" height="8" viewBox="0 0 12 8"
                fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path d="M1 1.5L6 6.5L11 1.5" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                  stroke-linejoin="round" />
              </svg>
            </button>

            <div :id="'dropdown-menu-' + dropdownId" class="dropdown-menu" :class="{ 'show': showSubmenu }" role="menu"
              @focusout="onDropdownFocusOut">
              <a href="#tentang" class="dropdown-link" role="menuitem" @click="closeMenuAndScroll"
                @keydown.tab="handleDropdownTab">Sejarah Koperasi ARM</a>
              <a href="#pengurus" class="dropdown-link" role="menuitem" @click="closeMenuAndScroll"
                @keydown.tab="handleDropdownTab">Pengurus</a>
              <a href="#about-section" class="dropdown-link" role="menuitem" @click="closeMenuAndScroll"
                @keydown.tab="handleDropdownTab">Visi & Misi</a>
            </div>
          </div>

          <a href="#layanan" class="navbar-link" @click="closeMenu" @focus="onLinkFocus">Produk & Layanan</a>
          <a href="https://athayarayamadani.co.id/kreditpensiun/auth/login" target="_blank" rel="noopener noreferrer"
            class="navbar-link" @click="closeMenu" @focus="onLinkFocus"
            style="color: gold; text-decoration: none; padding: 4px 8px; border-radius: 4px; transition: 0.2s;"
            onmouseover="this.style.backgroundColor='yellow'; this.style.color='darkblue'; this.style.textDecoration='underline';"
            onmouseout="this.style.backgroundColor='darkblue'; this.style.color='gold'; this.style.textDecoration='none';">
            Aplikasi Kresun
          </a>

          <a href="#kontak" class="navbar-link" @click="closeMenu" @focus="onLinkFocus">Kontak</a>
        </div>

        <button class="navbar-toggle" @click="toggleMenu" :class="{ 'navbar-toggle-open': isMenuOpen }"
          aria-label="Toggle navigation menu">
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
const showSubmenu = ref(false)
const dropdownId = Math.random().toString(36).substring(2, 9) // Unique ID for accessibility

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

const closeMenuAndScroll = () => {
  isMenuOpen.value = false
  showSubmenu.value = false
}

const onLinkFocus = () => {
  if (window.innerWidth <= 768) {
    showSubmenu.value = false; // Close submenu on mobile when focusing other links
  }
}

const handleDropdownTab = (e: KeyboardEvent) => {
  if (e.shiftKey) {
    // If shifting tab and on first item, close the dropdown
    const firstItem = (e.target as Element).parentElement?.firstElementChild;
    if (firstItem === e.target) {
      showSubmenu.value = false;
    }
  } else {
    // If tabbing and on last item, close the dropdown
    const lastItem = (e.target as Element).parentElement?.lastElementChild;
    if (lastItem === e.target) {
      showSubmenu.value = false;
    }
  }
}

const onDropdownFocusOut = (e: FocusEvent) => {
  // Close dropdown when focus moves outside of it
  const relatedTarget = e.relatedTarget as Node;
  const dropdown = e.currentTarget as HTMLElement;
  if (!dropdown.contains(relatedTarget)) {
    showSubmenu.value = false;
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  // Close dropdown when clicking outside
  document.addEventListener('click', (event) => {
    const target = event.target as HTMLElement;
    if (!target.closest('.navbar-dropdown')) {
      showSubmenu.value = false;
    }
  });
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  document.removeEventListener('click', () => { });
})
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background: rgba(10, 29, 55, 0.11);
  /* fallback */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  z-index: 1000;
  transition: all 0.3s ease;
}

.navbar-scrolled {
  background: rgba(10, 29, 55, 0.9);
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
  font-size: 1.1rem;
  font-weight: 1000;
  color: var(--accent-color);
  margin-bottom: 2px;
}

.brand-subtext {
  font-size: 0.8rem;
  font-weight: 800;
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
  display: flex;
  align-items: center;
  gap: 6px;
}

.navbar-link:hover {
  background-color: var(--accent-color);
  color: var(--primary-color);
}

.dropdown-button {
  cursor: pointer;
  background: none;
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  width: 100%;
  text-align: left;
  font-size: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.dropdown-icon {
  transition: transform 0.3s ease;
  color: var(--white);
}

.rotate-icon {
  transform: rotate(180deg);
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  background: var(--primary-color);
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  min-width: 200px;
  opacity: 0;
  visibility: hidden;
  transform: translateY(-10px);
  transition: all 0.3s ease;
  z-index: 1001;
}

.dropdown-menu.show {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

/* Position the dropdown relative to its parent */
.navbar-dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-link {
  display: block;
  padding: 12px 16px;
  color: var(--white);
  text-decoration: none;
  transition: background-color 0.3s ease;
  width: 100%;
  text-align: left;
}

.dropdown-link:hover {
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

  .dropdown-menu {
    position: static;
    transform: none;
    box-shadow: none;
    background: rgba(10, 29, 55, 0.9);
    margin-top: 8px;
  }
}
</style>