<template>
  <section id="testimoni" class="section testimonials">
    <div class="container">
      <div 
        class="section-header"
        v-motion
        :initial="{ opacity: 0, y: 30 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="200"
      >
        <h2 class="section-title">Testimoni Anggota</h2>
        <p class="section-subtitle">
          Dengarkan pengalaman para anggota yang telah merasakan manfaat bergabung dengan kami
        </p>
      </div>

      <div class="testimonials-slider">
        <div 
          class="slider-container"
          :style="{ transform: `translateX(-${currentSlide * 100}%)` }"
        >
          <div 
            v-for="(testimonial, index) in testimonials"
            :key="testimonial.id"
            class="testimonial-slide"
          >
            <div class="testimonial-card">
              <div class="testimonial-content">
                <div class="quote-icon">"</div>
                <p class="testimonial-text">{{ testimonial.text }}</p>
                <div class="testimonial-rating">
                  <span v-for="i in 5" :key="i" class="star" :class="{ 'filled': i <= testimonial.rating }">★</span>
                </div>
              </div>
              
              <div class="testimonial-author">
                <img :src="testimonial.avatar" :alt="testimonial.name" class="author-avatar">
                <div class="author-info">
                  <h4>{{ testimonial.name }}</h4>
                  <p>{{ testimonial.profession }}</p>
                  <span class="member-since">Anggota sejak {{ testimonial.memberSince }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="slider-controls">
          <button 
            class="slider-btn prev" 
            @click="previousSlide"
            :disabled="currentSlide === 0"
          >
            ‹
          </button>
          
          <div class="slider-dots">
            <button 
              v-for="(_, index) in testimonials"
              :key="index"
              class="slider-dot"
              :class="{ 'active': index === currentSlide }"
              @click="goToSlide(index)"
            ></button>
          </div>
          
          <button 
            class="slider-btn next" 
            @click="nextSlide"
            :disabled="currentSlide === testimonials.length - 1"
          >
            ›
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface Testimonial {
  id: number
  name: string
  profession: string
  text: string
  rating: number
  avatar: string
  memberSince: string
}

const currentSlide = ref(0)
let autoSlideInterval: number | null = null

const testimonials: Testimonial[] = [
  {
    id: 1,
    name: 'Budi Santoso',
    profession: 'Pengusaha Kuliner',
    text: 'Koperasi Athaya Raya Madani sangat membantu saya mengembangkan usaha kuliner. Proses pinjamannya mudah dan bunganya sangat kompetitif. Pelayanannya juga ramah dan profesional.',
    rating: 5,
    avatar: 'https://images.pexels.com/photos/2379004/pexels-photo-2379004.jpeg?auto=compress&cs=tinysrgb&w=150&h=150&fit=crop',
    memberSince: '2018'
  },
  {
    id: 2,
    name: 'Siti Nurhaliza',
    profession: 'Ibu Rumah Tangga',
    text: 'Simpanan berjangka di sini memberikan bunga yang lebih baik dari bank. Saya merasa aman menyimpan dana untuk pendidikan anak-anak. Terima kasih Koperasi Athaya!',
    rating: 5,
    avatar: 'https://images.pexels.com/photos/1130626/pexels-photo-1130626.jpeg?auto=compress&cs=tinysrgb&w=150&h=150&fit=crop',
    memberSince: '2019'
  },
  {
    id: 3,
    name: 'Ahmad Firdaus',
    profession: 'Karyawan Swasta',
    text: 'Program pensiun di koperasi ini sangat membantu saya mempersiapkan masa depan. Iurannya terjangkau dan manfaatnya jelas. Aplikasi digitalnya juga mudah digunakan.',
    rating: 4,
    avatar: 'https://images.pexels.com/photos/1222271/pexels-photo-1222271.jpeg?auto=compress&cs=tinysrgb&w=150&h=150&fit=crop',
    memberSince: '2020'
  },
  {
    id: 4,
    name: 'Maya Sari',
    profession: 'Pemilik Toko Fashion',
    text: 'Sebagai anggota baru, saya langsung merasakan pelayanan yang excellent. Pinjaman untuk modal usaha disetujui dengan cepat dan prosesnya transparan.',
    rating: 5,
    avatar: 'https://images.pexels.com/photos/1239291/pexels-photo-1239291.jpeg?auto=compress&cs=tinysrgb&w=150&h=150&fit=crop',
    memberSince: '2023'
  }
]

const nextSlide = () => {
  if (currentSlide.value < testimonials.length - 1) {
    currentSlide.value++
  } else {
    currentSlide.value = 0
  }
}

const previousSlide = () => {
  if (currentSlide.value > 0) {
    currentSlide.value--
  } else {
    currentSlide.value = testimonials.length - 1
  }
}

const goToSlide = (index: number) => {
  currentSlide.value = index
}

const startAutoSlide = () => {
  autoSlideInterval = setInterval(() => {
    nextSlide()
  }, 5000)
}

const stopAutoSlide = () => {
  if (autoSlideInterval) {
    clearInterval(autoSlideInterval)
    autoSlideInterval = null
  }
}

onMounted(() => {
  startAutoSlide()
})

onUnmounted(() => {
  stopAutoSlide()
})
</script>

<style scoped>
.testimonials {
  background: var(--primary-color);
  color: var(--white);
}

.testimonials .section-title {
  color: var(--white);
}

.testimonials .section-subtitle {
  color: rgba(255, 255, 255, 0.8);
}

.testimonials-slider {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
}

.slider-container {
  display: flex;
  transition: transform 0.5s ease;
}

.testimonial-slide {
  flex: 0 0 100%;
  padding: 0 1rem;
}

.testimonial-card {
  background: var(--white);
  border-radius: 16px;
  padding: 3rem;
  color: var(--primary-color);
  box-shadow: var(--shadow);
  margin: 1rem 0;
}

.quote-icon {
  font-size: 4rem;
  color: var(--accent-color);
  line-height: 1;
  margin-bottom: 1rem;
}

.testimonial-text {
  font-size: 1.2rem;
  line-height: 1.6;
  margin-bottom: 2rem;
  font-style: italic;
}

.testimonial-rating {
  margin-bottom: 2rem;
}

.star {
  font-size: 1.5rem;
  color: #E0E0E0;
  margin-right: 0.25rem;
}

.star.filled {
  color: var(--accent-color);
}

.testimonial-author {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.author-avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid var(--accent-color);
}

.author-info h4 {
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.author-info p {
  color: var(--gray-medium);
  margin-bottom: 0.5rem;
}

.member-since {
  font-size: 0.9rem;
  color: var(--accent-color);
  font-weight: 500;
}

.slider-controls {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  margin-top: 2rem;
}

.slider-btn {
  background: var(--accent-color);
  color: var(--primary-color);
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  font-size: 1.5rem;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
}

.slider-btn:hover:not(:disabled) {
  background: #E6C200;
  transform: scale(1.1);
}

.slider-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.slider-dots {
  display: flex;
  gap: 0.5rem;
}

.slider-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.5);
  cursor: pointer;
  transition: all 0.3s ease;
}

.slider-dot.active {
  background: var(--accent-color);
  transform: scale(1.2);
}

@media (max-width: 768px) {
  .testimonial-card {
    padding: 2rem;
  }
  
  .testimonial-author {
    flex-direction: column;
    text-align: center;
    gap: 1rem;
  }
  
  .slider-controls {
    gap: 1rem;
  }
  
  .slider-btn {
    width: 40px;
    height: 40px;
    font-size: 1.2rem;
  }
}
</style>