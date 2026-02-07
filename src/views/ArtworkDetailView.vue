<template>
  <div class="artwork-detail" v-if="piece">
    <div class="detail-header">
      <router-link to="/" hash="#gallery" class="back-link">&larr; Back to Gallery</router-link>
    </div>

    <div class="detail-content">
      <div class="detail-image-wrapper">
        <img
          :src="`/images/${piece.image}`"
          :alt="piece.title"
          class="detail-image"
        >
      </div>

      <div class="detail-info">
        <h1>{{ piece.title }}</h1>
        <p v-if="piece.medium" class="detail-medium">{{ piece.medium }}</p>
        <p v-if="piece.description" class="detail-description">{{ piece.description }}</p>

        <div class="detail-meta">
          <p class="detail-artist">By Jake Allen</p>
        </div>

        <router-link to="/" hash="#gallery" class="back-button">&larr; Back to Gallery</router-link>
      </div>
    </div>
  </div>

  <div class="artwork-detail artwork-not-found" v-else-if="loaded">
    <div class="detail-header">
      <router-link to="/" hash="#gallery" class="back-link">&larr; Back to Gallery</router-link>
    </div>
    <p>Artwork not found.</p>
  </div>
</template>

<script>
export default {
  name: 'ArtworkDetailView',
  data() {
    return {
      piece: null,
      loaded: false
    }
  },
  mounted() {
    this.loadArtwork()
  },
  watch: {
    '$route.params.id'() {
      this.loadArtwork()
    }
  },
  methods: {
    loadArtwork() {
      const id = parseInt(this.$route.params.id)
      fetch('/artwork.json')
        .then(response => response.json())
        .then(data => {
          this.piece = data.gallery.find(p => p.id === id) || null
          this.loaded = true
        })
        .catch(error => {
          console.error('Error loading artwork:', error)
          this.loaded = true
        })
    }
  }
}
</script>

<style scoped>
.artwork-detail {
  max-width: 1200px;
  margin: 0 auto;
  padding: 120px 2rem 4rem;
  min-height: 100vh;
}

.detail-header {
  margin-bottom: 2rem;
}

.back-link {
  display: inline-block;
  text-decoration: none;
  color: var(--color-text-light);
  font-size: 0.95rem;
  letter-spacing: 0.03em;
  transition: color 0.2s;
}

.back-link:hover {
  color: var(--color-text);
}

.detail-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

.detail-image-wrapper {
  position: sticky;
  top: 100px;
}

.detail-image {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 4px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.08);
}

.detail-info {
  padding-top: 1rem;
}

.detail-info h1 {
  font-family: var(--font-display);
  font-size: clamp(1.8rem, 4vw, 3rem);
  font-weight: 400;
  letter-spacing: -0.01em;
  margin-bottom: 1rem;
}

.detail-medium {
  font-size: 1.05rem;
  color: var(--color-text-light);
  margin-bottom: 1.5rem;
  letter-spacing: 0.02em;
}

.detail-description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--color-text);
  margin-bottom: 2rem;
}

.detail-meta {
  padding-top: 1.5rem;
  border-top: 1px solid var(--color-border);
  margin-bottom: 2rem;
}

.detail-artist {
  font-size: 0.95rem;
  color: var(--color-text-light);
  letter-spacing: 0.03em;
}

.back-button {
  display: inline-block;
  text-decoration: none;
  color: var(--color-text-light);
  font-size: 0.95rem;
  padding: 0.75rem 1.5rem;
  border: 1px solid var(--color-border);
  border-radius: 4px;
  transition: all 0.2s;
  letter-spacing: 0.03em;
}

.back-button:hover {
  color: var(--color-text);
  border-color: var(--color-text);
}

.artwork-not-found {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.artwork-not-found p {
  font-size: 1.2rem;
  color: var(--color-text-light);
}

@media (max-width: 768px) {
  .artwork-detail {
    padding: 100px 1.5rem 3rem;
  }

  .detail-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .detail-image-wrapper {
    position: static;
  }
}
</style>
