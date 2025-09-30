<template>
  <div class="maps-container">
    <iframe
      :src="mapSrc"
      width="100%"
      height="300"
      style="border: 0"
      allowfullscreen
      loading="lazy"
      referrerpolicy="no-referrer-when-downgrade"
    ></iframe>
  </div>
</template>

<script setup lang="ts">
interface Props {
  address?: string
  coordinates?: {
    lat: number
    lng: number
  }
}

const props = withDefaults(defineProps<Props>(), {
  address: 'KSP ATHAYA RAYA MADANI, 3M68+232, Jl. Venus Bar., Manjahlega, Kec. Rancasari, Kota Bandung, Jawa Barat 40286',
  coordinates: () => ({
    lat: -6.9398368,
    lng: 107.6653749
  })
})

const mapSrc = `https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3961.140394885761!2d107.6631861749825!3d-6.939836898780185!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e68e957c3058ff7%3A0x77bf730191df7f3d!2sKSP%20ATHAYA%20RAYA%20MADANI!5e0!3m2!1sid!2sid!4v1727438568000!5m2!1sid!2sid`
</script>

<style scoped>
.maps-container {
  height: 300px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

@media (max-width: 768px) {
  .maps-container {
    height: 200px;
  }
}
</style>