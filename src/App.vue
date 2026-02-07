<template>
  <div id="app">
    <header>
      <nav>
        <a href="#/" class="logo">JA</a>
        <ul>
          <li><a href="#gallery">Gallery</a></li>
          <li><a href="#about">About</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <section id="hero">
        <!-- Abstract background art -->
        <svg class="hero-background" viewBox="0 0 1000 1000" preserveAspectRatio="xMidYMid slice">
          <!-- Geometric shapes and lines -->
          <defs>
            <linearGradient id="gradientLine1" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" style="stop-color:#8b7355;stop-opacity:0.15" />
              <stop offset="100%" style="stop-color:#d4a574;stop-opacity:0.05" />
            </linearGradient>
            <linearGradient id="gradientLine2" x1="100%" y1="0%" x2="0%" y2="100%">
              <stop offset="0%" style="stop-color:#c9a961;stop-opacity:0.1" />
              <stop offset="100%" style="stop-color:#8b7355;stop-opacity:0.08" />
            </linearGradient>
          </defs>
          
          <!-- Large flowing lines -->
          <path d="M 0 200 Q 250 100, 500 250 T 1000 400" stroke="url(#gradientLine1)" stroke-width="5" fill="none" />
          <path d="M 1000 150 Q 750 300, 500 200 T 0 500" stroke="url(#gradientLine2)" stroke-width="4" fill="none" />
          <path d="M 0 600 L 1000 400" stroke="url(#gradientLine1)" stroke-width="3.5" fill="none" opacity="0.8" />
          
          <!-- Geometric shapes -->
          <circle cx="150" cy="200" r="80" fill="none" stroke="#a8956f" stroke-width="2.5" opacity="0.4" />
          <circle cx="850" cy="700" r="120" fill="none" stroke="#c9a961" stroke-width="2" opacity="0.35" />
          <rect x="700" y="100" width="200" height="200" fill="none" stroke="#8b7355" stroke-width="2.5" opacity="0.4" transform="rotate(25 800 200)" />
          <polygon points="200,800 300,700 350,850 280,900" fill="none" stroke="#a8956f" stroke-width="2" opacity="0.4" />
          
          <!-- Scattered abstract lines -->
          <line x1="0" y1="800" x2="300" y2="750" stroke="#c9a961" stroke-width="2" opacity="0.35" />
          <line x1="700" y1="950" x2="1000" y2="850" stroke="#8b7355" stroke-width="2.5" opacity="0.4" />
          <line x1="400" y1="0" x2="350" y2="400" stroke="#a8956f" stroke-width="2" opacity="0.3" />
          <line x1="600" y1="0" x2="700" y2="500" stroke="#c9a961" stroke-width="2" opacity="0.35" />
          
          <!-- Subtle dots -->
          <circle cx="100" cy="500" r="4" fill="#8b7355" opacity="0.4" />
          <circle cx="450" cy="150" r="3.5" fill="#a8956f" opacity="0.35" />
          <circle cx="900" cy="300" r="4" fill="#c9a961" opacity="0.4" />
          <circle cx="250" cy="900" r="3" fill="#8b7355" opacity="0.3" />
        </svg>
        
        <div class="hero-content">
          <h1>Jake Allen</h1>
          <p>Original artwork & illustrations</p>
        </div>
      </section>

      <Gallery></Gallery>
      <About></About>
      <Contact></Contact>
    </main>

    <footer>
      <p>&copy; 2026 Jake Allen. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import Gallery from './components/Gallery.vue'
import About from './components/About.vue'
import Contact from './components/Contact.vue'

export default {
  name: 'App',
  components: {
    Gallery,
    About,
    Contact
  }
}
</script>

<style scoped>
/* Header */
header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  background: rgba(250, 250, 250, 0.85);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(200, 200, 200, 0.3);
}

nav {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-family: var(--font-display);
  font-size: 1.5rem;
  text-decoration: none;
  color: var(--color-text);
}

nav ul {
  display: flex;
  list-style: none;
  gap: 2rem;
}

nav a {
  text-decoration: none;
  color: var(--color-text-light);
  font-size: 0.9rem;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  transition: color 0.2s;
}

nav a:hover {
  color: var(--color-text);
}

/* Main content */
main {
  margin-top: 0;
}

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
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  opacity: 0.75;
}

.hero-content {
  position: relative;
  z-index: 1;
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

/* Footer */
footer {
  text-align: center;
  padding: 2rem;
  color: var(--color-text-light);
  font-size: 0.85rem;
  border-top: 1px solid var(--color-border);
}
</style>
