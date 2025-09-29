<template>
  <section class="section stats">
    <div class="container">
      <div 
        class="stats-content"
        v-motion
        :initial="{ opacity: 0, y: 50 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="200"
      >
        <div class="stats-header">
          <h2>Kepercayaan dalam Angka</h2>
          <p>Pencapaian yang membanggakan berkat dukungan seluruh anggota</p>
        </div>

        <div class="stats-grid">
          <div 
            v-for="(stat, index) in stats"
            :key="stat.id"
            class="stat-item"

            :delay="400 + (index * 100)"
          >
            <div class="stat-icon" :style="{ background: stat.gradient }">
              {{ stat.icon }}
            </div>
            <div class="stat-content">
              <div class="stat-number" ref="statNumbers">
                {{ displayedNumbers[index] }}{{ stat.suffix }}
              </div>
              <div class="stat-label">{{ stat.label }}</div>
              <div class="stat-description">{{ stat.description }}</div>
            </div>
          </div>
        </div>

        <div class="stats-achievements">
          <h3>Penghargaan & Sertifikasi</h3>
          <div class="achievements-grid">
            <div 
              v-for="(achievement, index) in achievements"
              :key="achievement.id"
              class="achievement-item"
              v-motion
              :initial="{ opacity: 0, y: 30 }"
              :enter="{ opacity: 1, y: 0 }"
              :delay="800 + (index * 100)"
            >
              <div class="achievement-icon">{{ achievement.icon }}</div>
              <div class="achievement-content">
                <h4>{{ achievement.title }}</h4>
                <p>{{ achievement.description }}</p>
                <span class="achievement-year">{{ achievement.year }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, reactive } from 'vue'

interface Stat {
  id: number
  icon: string
  number: number
  suffix: string
  label: string
  description: string
  gradient: string
}

interface Achievement {
  id: number
  icon: string
  title: string
  description: string
  year: string
}

const displayedNumbers = reactive<number[]>([])

const stats: Stat[] = [
  {
    id: 1,
    icon: '👥',
    number: 15420,
    suffix: '+',
    label: 'Anggota Aktif',
    description: 'Tersebar di seluruh Jawa Barat',
    gradient: 'linear-gradient(135deg, #FFD700, #FFA000)'
  },
  {
    id: 2,
    icon: '🏢',
    number: 12,
    suffix: '',
    label: 'Kantor Cabang',
    description: 'Melayani di berbagai kota',
    gradient: 'linear-gradient(135deg, #4CAF50, #2E7D32)'
  },
  {
    id: 3,
    icon: '💰',
    number: 250,
    suffix: 'M',
    label: 'Total Pembiayaan',
    description: 'Dalam miliar rupiah per tahun',
    gradient: 'linear-gradient(135deg, #2196F3, #1565C0)'
  },
  {
    id: 4,
    icon: '⭐',
    number: 98,
    suffix: '%',
    label: 'Tingkat Kepuasan',
    description: 'Rating kepuasan anggota',
    gradient: 'linear-gradient(135deg, #9C27B0, #6A1B9A)'
  }
]

const achievements: Achievement[] = [
  {
    id: 1,
    icon: '🏆',
    title: 'Koperasi Berprestasi Terbaik',
    description: 'Penghargaan dari Dinas Koperasi Jawa Barat',
    year: '2023'
  },
  {
    id: 2,
    icon: '🛡️',
    title: 'Sertifikat ISO 9001:2015',
    description: 'Standar manajemen mutu internasional',
    year: '2022'
  },
  {
    id: 3,
    icon: '🌟',
    title: 'Top Digital Innovation',
    description: 'Inovasi layanan digital terbaik',
    year: '2023'
  },
  {
    id: 4,
    icon: '🤝',
    title: 'Koperasi Terpercaya',
    description: 'Sertifikat kepercayaan dari OJK',
    year: '2024'
  }
]

// Animation untuk counter number
const animateNumbers = () => {
  stats.forEach((stat, index) => {
    displayedNumbers[index] = 0
    const increment = stat.number / 100
    const timer = setInterval(() => {
      if (displayedNumbers[index] < stat.number) {
        displayedNumbers[index] = Math.min(displayedNumbers[index] + increment, stat.number)
        if (displayedNumbers[index] === stat.number) {
          clearInterval(timer)
        }
      }
    }, 20)
  })
}

onMounted(() => {
  // Initialize displayed numbers
  stats.forEach((_, index) => {
    displayedNumbers[index] = 0
  })
  
  // Start animation after component mounts
  setTimeout(() => {
    animateNumbers()
  }, 500)
})
</script>

<style scoped>
.stats {
  background: var(--gray-light);
  position: relative;
  overflow: hidden;
}

.stats::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="dots" width="20" height="20" patternUnits="userSpaceOnUse"><circle cx="10" cy="10" r="1" fill="rgba(10,29,55,0.05)"/></pattern></defs><rect width="100" height="100" fill="url(%23dots)"/></svg>');
}

.stats-content {
  position: relative;
  z-index: 2;
}

.stats-header {
  text-align: center;
  margin-bottom: 4rem;
}

.stats-header h2 {
  color: var(--primary-color);
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.stats-header p {
  color: var(--gray-medium);
  font-size: 1.2rem;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.stat-item {
  background: var(--white);
  padding: 2.5rem;
  border-radius: 16px;
  box-shadow: var(--shadow);
  text-align: center;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.stat-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--accent-color);
}

.stat-item:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-hover);
}

.stat-icon {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  margin: 0 auto 1.5rem;
  color: var(--white);
}

.stat-number {
  font-size: 3rem;
  font-weight: 700;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
  line-height: 1;
}

.stat-label {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
}

.stat-description {
  color: var(--gray-medium);
  font-size: 0.9rem;
}

.stats-achievements {
  background: var(--white);
  padding: 3rem;
  border-radius: 16px;
  box-shadow: var(--shadow);
}

.stats-achievements h3 {
  color: var(--primary-color);
  font-size: 1.8rem;
  font-weight: 600;
  text-align: center;
  margin-bottom: 2rem;
}

.achievements-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}

.achievement-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1.5rem;
  border: 2px solid var(--gray-light);
  border-radius: 12px;
  transition: all 0.3s ease;
}

.achievement-item:hover {
  border-color: var(--accent-color);
  background: var(--gray-light);
}

.achievement-icon {
  font-size: 2rem;
  flex-shrink: 0;
}

.achievement-content h4 {
  color: var(--primary-color);
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.achievement-content p {
  color: var(--gray-medium);
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.achievement-year {
  background: var(--accent-color);
  color: var(--primary-color);
  font-size: 0.8rem;
  font-weight: 600;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
}

@media (max-width: 768px) {
  .stats-header h2 {
    font-size: 2rem;
  }
  
  .stats-grid {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
  }
  
  .stat-item {
    padding: 2rem;
  }
  
  .stat-number {
    font-size: 2.5rem;
  }
  
  .stats-achievements {
    padding: 2rem;
  }
  
  .achievements-grid {
    grid-template-columns: 1fr;
  }
}
</style>