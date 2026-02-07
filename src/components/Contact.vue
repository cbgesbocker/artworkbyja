<template>
  <section id="contact">
    <h2>Contact</h2>
    <div class="contact-content">
      <p>Interested in purchasing a piece or commissioning work?</p>
      <a href="mailto:studioja@yahoo.com" class="btn">Get in Touch</a>
      <p style="margin-top: 1rem; font-size: 0.9rem; color: #666">
        Jake Allen<br />
        <a
          href="mailto:studioja@yahoo.com"
          style="color: #2a2a2a; text-decoration: none"
          >studioja@yahoo.com</a
        >
      </p>
      <div class="social-links">
        <a href="#" aria-label="Instagram">Instagram</a>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Contact",
};
</script>

<style scoped>
section {
  padding: 6rem 2rem;
  max-width: 1400px;
  margin: 0 auto;
}

#contact {
  text-align: center;
  background: #fff;
  border-radius: 8px;
  margin: 4rem auto;
  padding: 4rem 2rem;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.05);
}

#contact h2 {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  margin-bottom: 2rem;
}

.contact-content p {
  color: var(--color-text-light);
  margin-bottom: 2rem;
}

.btn {
  display: inline-block;
  padding: 1rem 2.5rem;
  background: var(--color-accent);
  color: #fff;
  text-decoration: none;
  border-radius: 4px;
  font-size: 0.9rem;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  transition: background 0.2s;
}

.btn:hover {
  background: #000;
}

.social-links {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
  gap: 2rem;
}

.social-links a {
  color: var(--color-text-light);
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.2s;
}

.social-links a:hover {
  color: var(--color-text);
}
</style>
