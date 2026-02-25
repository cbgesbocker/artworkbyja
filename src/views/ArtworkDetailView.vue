<template>
  <div class="artwork-detail" v-if="piece">
    <div class="detail-header">
      <router-link :to="{ path: '/', hash: '#gallery' }" class="back-link"
        >&larr; Back to Gallery</router-link
      >
    </div>

    <div class="detail-content">
      <div class="detail-image-wrapper">
        <!-- Image display with navigation -->
        <div class="image-container" v-if="allImages.length > 1">
          <button
            class="nav-btn prev-btn"
            @click="previousImage"
            title="Previous image (←)"
          >
            <span>‹</span>
          </button>
          <img
            :src="`/images/${activeImage}`"
            :alt="piece.title"
            class="detail-image"
          />
          <button
            class="nav-btn next-btn"
            @click="nextImage"
            title="Next image (→)"
          >
            <span>›</span>
          </button>
          <div class="image-counter">
            {{ currentImageIndex + 1 }} / {{ allImages.length }}
          </div>
        </div>
        <img
          v-else
          :src="`/images/${activeImage}`"
          :alt="piece.title"
          class="detail-image"
        />

        <!-- Thumbnail strip -->
        <div class="alt-images" v-if="allImages.length > 1">
          <button
            v-for="(img, idx) in allImages"
            :key="img"
            :class="['thumb-btn', activeImage === img ? 'active' : '']"
            @click="selectImage(idx)"
            :title="`View ${idx + 1} of ${allImages.length}`"
          >
            <img :src="`/images/${img}`" :alt="piece.title" />
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
            <div class="meta-row" v-if="piece.collaboration">
              <dt>Collaboration</dt>
              <dd>{{ piece.collaboration }}</dd>
            </div>
            <div class="meta-row" v-if="piece.artists && piece.artists.length">
              <dt>Artists</dt>
              <dd>{{ piece.artists.join(", ") }}</dd>
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
              <dd
                :class="[
                  'availability',
                  piece.availability === 'For Sale' ? 'for-sale' : 'sold',
                ]"
              >
                {{ piece.availability }}
              </dd>
            </div>
          </dl>
        </div>

        <router-link :to="{ path: '/', hash: '#gallery' }" class="back-button"
          >&larr; Back to Gallery</router-link
        >
      </div>
    </div>
  </div>

  <div class="artwork-detail artwork-not-found" v-else-if="loaded">
    <div class="detail-header">
      <router-link :to="{ path: '/', hash: '#gallery' }" class="back-link"
        >&larr; Back to Gallery</router-link
      >
    </div>
    <p>Artwork not found.</p>
  </div>
</template>

<script>
export default {
  name: "ArtworkDetailView",
  data() {
    return {
      piece: null,
      loaded: false,
      activeImage: null,
    };
  },
  computed: {
    allImages() {
      if (!this.piece) return [];
      return [this.piece.image, ...(this.piece.altImages || [])];
    },
    currentImageIndex() {
      return this.allImages.indexOf(this.activeImage);
    },
  },
  mounted() {
    this.loadArtwork();
    window.addEventListener("keydown", this.handleKeyboard);
  },
  beforeUnmount() {
    window.removeEventListener("keydown", this.handleKeyboard);
  },
  watch: {
    "$route.params.id"() {
      this.loadArtwork();
    },
  },
  methods: {
    loadArtwork() {
      const id = parseInt(this.$route.params.id);
      fetch("/artwork.json")
        .then((response) => response.json())
        .then((data) => {
          this.piece = data.gallery.find((p) => p.id === id) || null;
          this.activeImage = this.piece ? this.piece.image : null;
          this.loaded = true;
        })
        .catch((error) => {
          console.error("Error loading artwork:", error);
          this.loaded = true;
        });
    },
    previousImage() {
      const idx = this.currentImageIndex;
      if (idx > 0) {
        this.activeImage = this.allImages[idx - 1];
      }
    },
    nextImage() {
      const idx = this.currentImageIndex;
      if (idx < this.allImages.length - 1) {
        this.activeImage = this.allImages[idx + 1];
      }
    },
    selectImage(index) {
      this.activeImage = this.allImages[index];
    },
    handleKeyboard(e) {
      if (e.key === "ArrowLeft") {
        this.previousImage();
      } else if (e.key === "ArrowRight") {
        this.nextImage();
      }
    },
  },
};
</script>

<style scoped>
.artwork-detail {
  max-width: 1600px;
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
  grid-template-columns: 1.3fr 1fr;
  gap: 4rem;
  align-items: start;
}

.detail-image-wrapper {
  position: sticky;
  top: 100px;
  display: flex;
  flex-direction: column;
}

.detail-image-wrapper > .detail-image {
  max-height: 75vh;
  object-fit: contain;
  width: 100%;
}

.image-container {
  position: relative;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  max-height: 75vh;
}

.image-container {
  position: relative;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.detail-image {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 4px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.08);
}

.image-container .detail-image {
  flex: 1;
  max-height: 75vh;
  object-fit: contain;
}

.nav-btn {
  flex-shrink: 0;
  width: 44px;
  height: 44px;
  border: 1px solid var(--color-border);
  border-radius: 4px;
  background: rgba(250, 250, 250, 0.8);
  backdrop-filter: blur(10px);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text);
  font-size: 1.5rem;
  transition: all 0.2s;
}

.nav-btn:hover {
  background: rgba(250, 250, 250, 0.95);
  border-color: var(--color-text);
}

.image-counter {
  position: absolute;
  bottom: 12px;
  right: 12px;
  font-size: 0.78rem;
  background: rgba(26, 26, 26, 0.7);
  color: rgba(250, 250, 250, 0.9);
  padding: 0.4rem 0.8rem;
  border-radius: 4px;
  letter-spacing: 0.05em;
  font-weight: 500;
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
