<template>
  <div>
    <ImageMagnifier 
      src="https://wallpapers.com/images/featured/japon-4k-qbc6mlnwowjbszld.jpg"
      zoomLevel="2"
      zoomWidth="350"
      zoomHeight="450"
    />
  </div>
</template>

<script setup>
import ImageMagnifier from "./components/ImageMagnifier.vue";
</script>

<style scoped>

div {
  display: flex;
  justify-content: center;
  width: 1200px;
  margin: auto;
}

img {
  object-fit: cover;
  cursor: zoom-in;
}
</style>
