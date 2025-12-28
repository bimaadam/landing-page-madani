<template>
  <section id="struktur-organisasi" class="py-5">
    <div class="container">
      <div class="text-center mb-5">
        <h2 class="fw-bold">Struktur Organisasi</h2>
        <p class="text-muted">Struktur Kepengurusan Koperasi Madani</p>
      </div>

      <div class="structure-container">
        <div class="structure-image">
          <img src="/struktur1.jpg" alt="Struktur Organisasi 1" />
        </div>
        <div class="structure-image">
          <img src="/struktur2.jpg" alt="Struktur Organisasi 2" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// No script needed
</script>

<style scoped>
.py-5 {
  padding: 4rem 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.text-center {
  text-align: center;
}

.mb-5 {
  margin-bottom: 3rem;
}

.fw-bold {
  font-weight: 700;
  font-size: 2rem;
  color: var(--primary-color);
}

.text-muted {
  color: var(--gray-medium);
  font-size: 1.1rem;
}

.structure-container {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  max-width: 1000px;
  margin: 0 auto;
}

.structure-image {
  width: 100%;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.structure-image img {
  width: 100%;
  height: auto;
  display: block;
}

@media (max-width: 768px) {
  .fw-bold {
    font-size: 1.5rem;
  }
  
  .text-muted {
    font-size: 1rem;
  }
}
</style>
