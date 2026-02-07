<template>
  <section id="gallery">
    <h2>Gallery</h2>
    <div class="gallery-grid">
      <router-link
        v-for="piece in gallery"
        :key="piece.id"
        :to="`/artwork/${piece.id}`"
        class="artwork"
      >
        <img
          :src="`/images/${piece.image}`"
          :alt="piece.title"
        >
        <div class="artwork-info">
          <h3>{{ piece.title }}</h3>
          <p>{{ piece.medium }}</p>
        </div>
      </router-link>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Gallery',
  data() {
    return {
      gallery: []
    }
  },
  mounted() {
    this.loadGallery()
  },
  methods: {
    loadGallery() {
      fetch('/artwork.json')
        .then(response => response.json())
        .then(data => {
          this.gallery = data.gallery
        })
        .catch(error => console.error('Error loading gallery:', error))
    }
  }
}
</script>

<style scoped>
section {
  padding: 6rem 2rem;
  max-width: 1400px;
  margin: 0 auto;
}

#gallery {
  text-align: center;
}

#gallery h2 {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  margin-bottom: 2rem;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.artwork {
  position: relative;
  overflow: hidden;
  background: #fff;
  border-radius: 4px;
  box-shadow: 0 2px 20px rgba(0,0,0,0.05);
  transition: transform 0.3s, box-shadow 0.3s;
  text-decoration: none;
  color: inherit;
  display: block;
  cursor: pointer;
}

.artwork:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 40px rgba(0,0,0,0.1);
}

.artwork img {
  width: 100%;
  height: 350px;
  object-fit: cover;
  display: block;
}

.artwork-info {
  padding: 1.5rem;
  text-align: left;
}

.artwork-info h3 {
  font-size: 1.1rem;
  margin-bottom: 0.25rem;
}

.artwork-info p {
  color: var(--color-text-light);
  font-size: 0.9rem;
}
</style>
