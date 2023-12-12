<template>
  <main>
    <h1> Foods! </h1>
    <div class="image-container">
      <img :src="currentImage" @mouseover="hoverImage" @mouseleave="leaveImage"  alt="Foods!"/>
    </div>
    <button @click="previousImage">Previous</button>
    <button @click="nextImage">Next</button>
    <section>
      <h2>What's happening?</h2>
      <p>There are 4 food pictures, you can browse them all by click previous and next. You can also hover it to see the previous one, like magic wand.</p>
    </section>
  </main>
</template>

<script>
import ImgData from '@/assets/imagelinks.json';

export default {
  name: 'App',
  data() {
    return {
      images: ImgData.menu_pics.map(url => ({ original: url, hover: url, current: url })),
      currentIndex: 0,
    };
  },
  computed: {
    currentImage() {
      return this.images[this.currentIndex].current;
    },
    previousIndex() {
      return (this.currentIndex - 1 + this.images.length) % this.images.length;
    },
  },
  methods: {
    hoverImage() {
      this.currentIndex = this.previousIndex;
    },
    leaveImage() {
      // Do nothing
    },
    previousImage() {
      this.currentIndex = this.previousIndex;
    },
    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    },
  },
};
</script>

<style>
.image-container {
  display: grid;
  grid-gap: 10px; /* Add space between images */
  padding: 30px; /* Add padding around the image container */
}

.image-container img {
  align-self: center;
  width: 500px;
  height: auto;
  transition: transform 0.3s ease;
}

.image-container img:hover {
  transform: scale(1.1);
}
</style>
