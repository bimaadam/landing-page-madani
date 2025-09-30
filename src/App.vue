<template>
  <div id="app">
    <Navbar />
    <main>
      <Hero />
      <About />
      <Services />
      <Testimonials />
      <Stats />
      <Divisions />
      <Partners />
      <Contact />
    </main>
    <Footer />
  </div>
</template>

<script setup lang="ts">
import { MotionPlugin } from '@vueuse/motion'
import { createApp, onMounted } from 'vue'

import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import About from '@/components/About.vue'
import Services from '@/components/Services.vue'
import Testimonials from '@/components/Testimonials.vue'
import Stats from '@/components/Stats.vue'
import Contact from '@/components/Contact.vue'
import Footer from '@/components/Footer.vue'
import Divisions from './components/Divisions.vue'
import Partners from './components/Partners.vue'


// Register motion plugin for smooth animations
const app = createApp({})
app.use(MotionPlugin)

// Simple utility to create/update meta tags
function upsertMeta(options: { name?: string; property?: string; content: string }) {
  const selector = options.name ? `meta[name="${options.name}"]` : `meta[property="${options.property}"]`
  let el = document.head.querySelector(selector) as HTMLMetaElement | null
  if (!el) {
    el = document.createElement('meta')
    if (options.name) el.setAttribute('name', options.name)
    if (options.property) el.setAttribute('property', options.property)
    document.head.appendChild(el)
  }
  el.setAttribute('content', options.content)
}

// Create or update a canonical link
function upsertCanonical(href: string) {
  let link = document.head.querySelector('link[rel="canonical"]') as HTMLLinkElement | null
  if (!link) {
    link = document.createElement('link')
    link.setAttribute('rel', 'canonical')
    document.head.appendChild(link)
  }
  link.setAttribute('href', href)
}

onMounted(() => {
  // Basic SEO / Open Graph / Twitter meta
  const title = 'Koperasi Athaya Raya Madani Bandung'
  const description = 'Koperasi Athaya Raya Madani adalah solusi keuangan terpercaya di Bandung, menyediakan layanan simpan pinjam dengan bunga kompetitif dan pelayanan profesional.'
  const url = window.location.href
  const image = `${window.location.origin}/social-preview.png` // adjust path if needed
  const keywords = 'koperasi, simpan pinjam, pembiayaan, keuangan, madani, bandung, koperasi syariah'

  // Document title
  document.title = title

  // Standard meta
  upsertMeta({ name: 'description', content: description })
  upsertMeta({ name: 'keywords', content: keywords })
  upsertMeta({ name: 'author', content: 'Madani' })
  upsertCanonical(url)

  // Open Graph
  upsertMeta({ property: 'og:title', content: title })
  upsertMeta({ property: 'og:description', content: description })
  upsertMeta({ property: 'og:type', content: 'website' })
  upsertMeta({ property: 'og:url', content: url })
  upsertMeta({ property: 'og:image', content: image })

  // Twitter Card
  upsertMeta({ name: 'twitter:card', content: 'summary_large_image' })
  upsertMeta({ name: 'twitter:title', content: title })
  upsertMeta({ name: 'twitter:description', content: description })
  upsertMeta({ name: 'twitter:image', content: image })
})
</script>

<style>
/* Global smooth scrolling for anchor links */
html {
  scroll-behavior: smooth;
}

/* Ensure full height layout */
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

main {
  flex: 1;
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: var(--gray-light);
}

::-webkit-scrollbar-thumb {
  background: var(--primary-color);
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: var(--light-blue);
}

/* Loading animation */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in-up {
  animation: fadeInUp 0.6s ease forwards;
}

/* Utility classes */
.text-center {
  text-align: center;
}

.text-left {
  text-align: left;
}

.text-right {
  text-align: right;
}

.mb-1 { margin-bottom: 0.25rem; }
.mb-2 { margin-bottom: 0.5rem; }
.mb-3 { margin-bottom: 1rem; }
.mb-4 { margin-bottom: 1.5rem; }
.mb-5 { margin-bottom: 3rem; }

.mt-1 { margin-top: 0.25rem; }
.mt-2 { margin-top: 0.5rem; }
.mt-3 { margin-top: 1rem; }
.mt-4 { margin-top: 1.5rem; }
.mt-5 { margin-top: 3rem; }

.p-1 { padding: 0.25rem; }
.p-2 { padding: 0.5rem; }
.p-3 { padding: 1rem; }
.p-4 { padding: 1.5rem; }
.p-5 { padding: 3rem; }

/* Accessibility improvements */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

/* Focus styles for better accessibility */
button:focus,
input:focus,
textarea:focus,
select:focus,
a:focus {
  outline: 2px solid var(--accent-color);
  outline-offset: 2px;
}

/* High contrast mode support */
@media (prefers-contrast: high) {
  .btn-primary {
    border: 2px solid var(--primary-color);
  }
  
  .btn-secondary {
    background-color: var(--white);
    color: var(--primary-color);
    border: 2px solid var(--primary-color);
  }
}
</style>