<template>
  <section class="section partners">
    <div class="container">
      <div class="partners-header">
        <h2>Mitra Kerjasama</h2>
        <p>Daftar perusahaan yang menjalin kerjasama strategis dengan koperasi kami</p>
      </div>

      <div class="partners-carousel">
        <div class="carousel-wrapper">
          <div class="carousel-track" :style="{ transform: `translateX(${translateX}px)` }">
            <!-- Duplicate items for continuous scrolling effect -->
            <div 
              v-for="(partner, index) in [...partners, ...partners]" 
              :key="`${partner.id}-${Math.floor(index/2)}`"
              class="carousel-item"
            >
              <div class="partner-logo">
                <img 
                  :src="partner.logo" 
                  :alt="partner.name"
                  @error="handleImageError"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface Partner {
  id: number
  name: string
  logo: string
}

const partners: Partner[] = [
  {
    id: 1,
    name: 'Partner 1',
    logo: '/partner/bprtas.png'
  },
  {
    id: 2,
    name: 'Partner 2',
    logo: '/partner/car.png'
  },
  {
    id: 3,
    name: 'Partner 3',
    logo: '/partner/cikarang.png'
  },
  {
    id: 4,
    name: 'Partner 4',
    logo: '/partner/dassa.png'
  },
  {
    id: 5,
    name: 'Partner 5',
    logo: '/partner/nbp.png'
  },
  {
    id: 6,
    name: 'Partner 6',
    logo: '/partner/panjawan.png'
  },
  {
    id: 7,
    name: 'Partner 7',
    logo: '/partner/sam.png'
  },
  {
    id: 8,
    name: 'Partner 8',
    logo: '/partner/sinarterang.png'
  },
  {
    id: 9,
    name: 'Partner 9',
    logo: '/partner/siwa.png'
  },
  {
    id: 10,
    name: 'Partner 10',
    logo: '/partner/vima.png'
  }
]

const translateX = ref(0)
let animationFrameId: number
let lastTime = 0
const speed = 0.5 // Kecepatan animasi

const animate = (timestamp: number) => {
  if (!lastTime) lastTime = timestamp
  const elapsed = timestamp - lastTime
  
  // Update posisi berdasarkan waktu yang berlalu
  translateX.value -= speed * (elapsed / 16) // 16 adalah waktu frame rata-rata untuk 60fps
  
  // Reset posisi ketika melewati setengah dari total width agar terus berjalan
  const totalItems = partners.length
  const itemWidth = 200 // lebar item + gap (180 + 20)
  const halfTrackWidth = (totalItems * itemWidth) / 2
  
  if (Math.abs(translateX.value) >= halfTrackWidth) {
    translateX.value = 0
  }
  
  lastTime = timestamp
  animationFrameId = requestAnimationFrame(animate)
}

const handleImageError = (event: Event) => {
  const target = event.target as HTMLImageElement
  // Placeholder SVG sebagai fallback
  target.src = 'data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAwIiBoZWlnaHQ9IjEwMCIgdmlld0JveD0iMCAwIDIwMCAxMDAiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PHJlY3Qgd2lkdGg9IjIwMCIgaGVpZ2h0PSIxMDAiIGZpbGw9IiNGNUY1RjUiLz48dGV4dCB4PSIxMDAiIHk9IjUwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBkb21pbmFudC1iYXNlbGluZT0iY2VudHJhbCIgZmlsbD0iIzk5OTk5OSI+UGFydG5lciBMb2dvPC90ZXh0Pjwvc3ZnPg=='
}

onMounted(() => {
  lastTime = 0
  animationFrameId = requestAnimationFrame(animate)
})

onUnmounted(() => {
  cancelAnimationFrame(animationFrameId)
})
</script>

<style scoped>
.partners {
  background: var(--white);
  padding: 4rem 0;
}

.partners-header {
  text-align: center;
  margin-bottom: 3rem;
}

.partners-header h2 {
  color: var(--primary-color);
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.partners-header p {
  color: var(--gray-medium);
  font-size: 1.2rem;
}

.partners-carousel {
  overflow: hidden;
  padding: 2rem 0;
}

.carousel-wrapper {
  overflow: hidden;
  width: 100%;
}

.carousel-track {
  display: flex;
  transition: transform 0.05s linear; /* Transisi halus untuk animasi */
}

.carousel-item {
  flex: 0 0 auto;
  width: 480px;
  margin-right: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.partner-logo {
  width: 100%;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--gray-light);
  border-radius: 8px;
  padding: 1rem;
  transition: all 0.3s ease;
}

.partner-logo:hover {
  transform: scale(1.05);
  background: var(--white);
  box-shadow: var(--shadow-hover);
}

.partner-logo img {
  max-width: 100%;
  max-height: 80px;
  object-fit: contain;
}

/* Animation for the carousel */
@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .partners-header h2 {
    font-size: 2rem;
  }
  
  .carousel-item {
    width: 140px;
    margin-right: 15px;
  }
  
  .partner-logo {
    height: 80px;
  }
  
  .partner-logo img {
    max-height: 60px;
  }
}
</style>