<template>
  <div>
    <section id="hero">
      <!-- Abstract background art -->

      <div class="hero-content">
        <h1>Jake Allen</h1>
        <p>Original artwork & illustrations</p>
      </div>
      <img src="/images/banner.png" alt="Hero banner" class="hero-banner" />
    </section>

    <Gallery></Gallery>
    <About></About>
    <Contact></Contact>
  </div>
</template>

<script>
import Gallery from "../components/Gallery.vue";
import About from "../components/About.vue";
import Contact from "../components/Contact.vue";

export default {
  name: "HomeView",
  components: {
    Gallery,
    About,
    Contact,
  },
};
</script>

<style scoped>
/* Hero */
#hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding-top: 80px;
  padding-left: 2rem;
  padding-right: 2rem;
  padding-bottom: 6rem;
  overflow: hidden;
  background: linear-gradient(135deg, #f5fbfd 0%, #eef7f9 100%);
}

.hero-banner {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 200px;
  object-fit: cover;
  z-index: 1;
  opacity: 0.8;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 2;
  opacity: 0.6;
}

.hero-content {
  position: relative;
  z-index: 3;
}

#hero h1 {
  font-size: clamp(2.5rem, 8vw, 5rem);
  letter-spacing: -0.02em;
}

#hero p {
  font-size: 1.25rem;
  color: var(--color-text-light);
  margin-top: 1rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}
</style>
