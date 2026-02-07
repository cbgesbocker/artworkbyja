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
        <h1>Jake Allen</h1>
        <p>Original artwork & illustrations</p>
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
  background: rgba(250, 250, 250, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--color-border);
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
