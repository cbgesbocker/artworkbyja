<template>
  <section id="about">
    <h2>About the Artist</h2>
    <div class="about-content">
      <img
        v-if="artistPhoto"
        :src="`/images/${artistPhoto}`"
        alt="Jake Allen"
        class="artist-photo"
      />
      <div class="about-text">
        <p v-if="artistBio">{{ artistBio }}</p>
        <p v-else>Loading artist info...</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "About",
  data() {
    return {
      artistBio: "",
      artistPhoto: "artist.JPG",
    };
  },
  mounted() {
    this.loadArtistInfo();
  },
  methods: {
    loadArtistInfo() {
      fetch("/artwork.json")
        .then((response) => response.json())
        .then((data) => {
          this.artistBio = data.artist.bio;
        })
        .catch((error) => console.error("Error loading artist info:", error));
    },
  },
};
</script>

<style scoped>
section {
  padding: 6rem 2rem;
  max-width: 1400px;
  margin: 0 auto;
}

#about {
  text-align: center;
}

#about h2 {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  margin-bottom: 2rem;
}

.about-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3rem;
  margin-top: 3rem;
}

@media (min-width: 768px) {
  .about-content {
    flex-direction: row;
    text-align: left;
  }
}

.artist-photo {
  width: 300px;
  height: 300px;
  object-fit: cover;
  border-radius: 50%;
}

.about-text {
  max-width: 900px;
}

.about-text p {
  margin-bottom: 1rem;
  color: var(--color-text-light);
}

.artist-photo[src*="artist"] {
  background: linear-gradient(135deg, #e0e0e0 0%, #f5f5f5 100%);
}
</style>
