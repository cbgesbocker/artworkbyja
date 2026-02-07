<template>
  <div id="app">
    <header>
      <nav>
        <router-link to="/" class="logo">JA</router-link>
        <ul>
          <li><a href="#" @click.prevent="scrollTo('gallery')">Gallery</a></li>
          <li><a href="#" @click.prevent="scrollTo('about')">About</a></li>
          <li><a href="#" @click.prevent="scrollTo('contact')">Contact</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <router-view></router-view>
    </main>

    <footer>
      <p>&copy; 2026 Jake Allen. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
    scrollTo(sectionId) {
      // If we're not on the home page, navigate there first
      if (this.$route.path !== '/') {
        this.$router.push('/').then(() => {
          this.$nextTick(() => {
            const el = document.getElementById(sectionId)
            if (el) {
              el.scrollIntoView({ behavior: 'smooth' })
            }
          })
        })
      } else {
        const el = document.getElementById(sectionId)
        if (el) {
          el.scrollIntoView({ behavior: 'smooth' })
        }
      }
    }
  }
};
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

/* Footer */
footer {
  text-align: center;
  padding: 2rem;
  color: var(--color-text-light);
  font-size: 0.85rem;
  border-top: 1px solid var(--color-border);
}
</style>
