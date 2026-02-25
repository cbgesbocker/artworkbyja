<template>
  <div>
    <section id="hero">
      <!-- Banner image -->
      <img src="/images/banner.png" alt="Hero banner" class="hero-banner" />

      <!-- Abstract background art -->
      <svg
        class="hero-background"
        viewBox="0 0 1000 1000"
        preserveAspectRatio="xMidYMid slice"
      >
        <defs>
          <linearGradient
            id="gradientLine1"
            x1="0%"
            y1="0%"
            x2="100%"
            y2="100%"
          >
            <stop
              offset="0%"
              style="stop-color: #1A7A99; stop-opacity: 0.2"
            />
            <stop
              offset="100%"
              style="stop-color: #0F5F7D; stop-opacity: 0.08"
            />
          </linearGradient>
          <linearGradient
            id="gradientLine2"
            x1="100%"
            y1="0%"
            x2="0%"
            y2="100%"
          >
            <stop
              offset="0%"
              style="stop-color: #2E9FB0; stop-opacity: 0.15"
            />
            <stop
              offset="100%"
              style="stop-color: #1A7A99; stop-opacity: 0.1"
            />
          </linearGradient>
        </defs>

        <!-- Large flowing lines -->
        <path
          d="M 0 200 Q 250 100, 500 250 T 1000 400"
          stroke="url(#gradientLine1)"
          stroke-width="3.5"
          fill="none"
        />
        <path
          d="M 1000 150 Q 750 300, 500 200 T 0 500"
          stroke="url(#gradientLine2)"
          stroke-width="3"
          fill="none"
        />
        <path
          d="M 0 600 L 1000 400"
          stroke="url(#gradientLine1)"
          stroke-width="2.5"
          fill="none"
          opacity="0.7"
        />

        <!-- Geometric shapes -->
        <circle
          cx="150"
          cy="200"
          r="80"
          fill="none"
          stroke="#2E9FB0"
          stroke-width="1.8"
          opacity="0.3"
        />
        <circle
          cx="850"
          cy="700"
          r="120"
          fill="none"
          stroke="#1A7A99"
          stroke-width="1.5"
          opacity="0.25"
        />
        <rect
          x="700"
          y="100"
          width="200"
          height="200"
          fill="none"
          stroke="#0F5F7D"
          stroke-width="1.8"
          opacity="0.3"
          transform="rotate(25 800 200)"
        />
        <polygon
          points="200,800 300,700 350,850 280,900"
          fill="none"
          stroke="#2E9FB0"
          stroke-width="1.5"
          opacity="0.3"
        />

        <!-- Scattered abstract lines -->
        <line
          x1="0"
          y1="800"
          x2="300"
          y2="750"
          stroke="#2E9FB0"
          stroke-width="1.5"
          opacity="0.25"
        />
        <line
          x1="700"
          y1="950"
          x2="1000"
          y2="850"
          stroke="#0F5F7D"
          stroke-width="1.8"
          opacity="0.3"
        />
        <line
          x1="400"
          y1="0"
          x2="350"
          y2="400"
          stroke="#1A7A99"
          stroke-width="1.5"
          opacity="0.2"
        />
        <line
          x1="600"
          y1="0"
          x2="700"
          y2="500"
          stroke="#2E9FB0"
          stroke-width="1.5"
          opacity="0.25"
        />

        <!-- Subtle dots -->
        <circle cx="100" cy="500" r="3" fill="#0F5F7D" opacity="0.3" />
        <circle cx="450" cy="150" r="2.5" fill="#1A7A99" opacity="0.25" />
        <circle cx="900" cy="300" r="3" fill="#2E9FB0" opacity="0.3" />
        <circle cx="250" cy="900" r="2" fill="#0F5F7D" opacity="0.2" />
      </svg>

      <div class="hero-content">
        <h1>Jake Allen</h1>
        <p>Original artwork & illustrations</p>
      </div>
    </section>

    <Gallery></Gallery>
    <About></About>
    <Contact></Contact>
  </div>
</template>

<script>
import Gallery from '../components/Gallery.vue'
import About from '../components/About.vue'
import Contact from '../components/Contact.vue'

export default {
  name: 'HomeView',
  components: {
    Gallery,
    About,
    Contact
  }
}
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
