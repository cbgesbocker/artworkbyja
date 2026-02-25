<template>
  <div class="artwork-detail" v-if="piece">
    <div class="detail-header">
      <router-link :to="{ path: '/', hash: '#gallery' }" class="back-link">&larr; Back to Gallery</router-link>
    </div>

    <div class="detail-content">
      <div class="detail-image-wrapper">
        <img
          :src="`/images/${activeImage}`"
          :alt="piece.title"
          class="detail-image"
        >
        <div class="alt-images" v-if="piece.altImages && piece.altImages.length">
          <button
            :class="['thumb-btn', activeImage === piece.image ? 'active' : '']"
            @click="activeImage = piece.image"
          >
            <img :src="`/images/${piece.image}`" :alt="piece.title">
          </button>
          <button
            v-for="alt in piece.altImages"
            :key="alt"
            :class="['thumb-btn', activeImage === alt ? 'active' : '']"
            @click="activeImage = alt"
          >
            <img :src="`/images/${alt}`" :alt="piece.title + ' alternate view'">
          </button>
        </div>
      </div>

      <div class="detail-info">
        <h1>{{ piece.title }}</h1>

        <div class="detail-meta">
          <dl class="meta-list">
            <div class="meta-row" v-if="piece.year">
              <dt>Year</dt>
              <dd>{{ piece.year }}</dd>
            </div>
            <div class="meta-row" v-if="piece.dimensions">
              <dt>Dimensions</dt>
              <dd>{{ piece.dimensions }}</dd>
            </div>
            <div class="meta-row" v-if="piece.material">
              <dt>Material</dt>
              <dd>{{ piece.material }}</dd>
            </div>
            <div class="meta-row" v-if="piece.featuredAt">
              <dt>Featured at</dt>
              <dd>{{ piece.featuredAt }}</dd>
            </div>
            <div class="meta-row" v-if="piece.availability">
              <dt>Availability</dt>
              <dd :class="['availability', piece.availability === 'For Sale' ? 'for-sale' : 'sold']">
                {{ piece.availability }}
              </dd>
            </div>
          </dl>
        </div>

        <router-link :to="{ path: '/', hash: '#gallery' }" class="back-button">&larr; Back to Gallery</router-link>
      </div>
    </div>
  </div>

  <div class="artwork-detail artwork-not-found" v-else-if="loaded">
    <div class="detail-header">
      <router-link :to="{ path: '/', hash: '#gallery' }" class="back-link">&larr; Back to Gallery</router-link>
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
      loaded: false,
      activeImage: null
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
          this.activeImage = this.piece ? this.piece.image : null
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

/* Alternate image thumbnails */
.alt-images {
  display: flex;
  gap: 0.75rem;
  margin-top: 1rem;
}

.thumb-btn {
  width: 64px;
  height: 64px;
  padding: 0;
  border: 2px solid var(--color-border);
  border-radius: 4px;
  overflow: hidden;
  cursor: pointer;
  background: none;
  transition: border-color 0.2s;
  flex-shrink: 0;
}

.thumb-btn img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.thumb-btn.active {
  border-color: var(--color-text);
}

.thumb-btn:hover:not(.active) {
  border-color: var(--color-text-light);
}

.detail-info {
  padding-top: 1rem;
}

.detail-info h1 {
  font-family: var(--font-display);
  font-size: clamp(1.8rem, 4vw, 3rem);
  font-weight: 400;
  letter-spacing: -0.01em;
  margin-bottom: 2rem;
}

/* Metadata table */
.detail-meta {
  border-top: 1px solid var(--color-border);
  margin-bottom: 2.5rem;
}

.meta-list {
  display: flex;
  flex-direction: column;
}

.meta-row {
  display: grid;
  grid-template-columns: 130px 1fr;
  gap: 1rem;
  padding: 0.85rem 0;
  border-bottom: 1px solid var(--color-border);
}

.meta-row dt {
  font-size: 0.78rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--color-text-light);
  padding-top: 0.1em;
}

.meta-row dd {
  font-size: 0.97rem;
  color: var(--color-text);
  margin: 0;
}

.availability {
  font-weight: 500;
  letter-spacing: 0.03em;
}

.availability.for-sale {
  color: #2d6a4f;
}

.availability.sold {
  color: var(--color-text-light);
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

  .meta-row {
    grid-template-columns: 110px 1fr;
  }
}
</style>
