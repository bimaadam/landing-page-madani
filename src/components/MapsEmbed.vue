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
  address: 'Jl. Cipamokolan No.8 RT.003 RW.001 Kel. Cipamokolan Kec. Rancasari Kota Bandung 40292',
  coordinates: () => ({
    lat: -6.9398368,
    lng: 107.6653749
  })
})

const mapSrc = `https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3960.5962447544816!2d107.67463097432542!3d-6.938762567922693!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e68c374cccff485%3A0xb4e03563cc9cd888!2sBank%20BRI%20CRM%20-%20BRI%20UNIT%20RIUNG!5e0!3m2!1sen!2sid!4v1766913265538!5m2!1sen!2sid`
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