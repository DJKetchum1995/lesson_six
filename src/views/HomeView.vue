<script setup lang="ts">
import { computed, ref, watchEffect } from 'vue'

const theme = ref<'dark' | 'mint'>('dark')

const themeIcon = computed(() => (theme.value === 'dark' ? '☀' : '☾'))
const themeLabel = computed(() =>
  theme.value === 'dark' ? 'Switch to Mint Green Mode' : 'Switch to Dark Mode'
)

const toggleTheme = () => {
  theme.value = theme.value === 'dark' ? 'mint' : 'dark'
}

const links = [
  {
    label: 'Portfolio',
    href: 'https://davidketchum.design',
  },
  {
    label: 'Dribbble',
    href: 'https://dribbble.com/davidketchum',
  },
  {
    label: 'LinkedIn',
    href: 'https://linkedin.com/in/david-ketchum',
  },
  {
    label: 'Email',
    href: 'mailto:david.ketchum@slalom.com',
  },
]

watchEffect(() => {
  document.documentElement.setAttribute('data-theme', theme.value)
})
</script>

<template>
  <main class="page-shell">
    <section class="profile-card">
      <div class="theme-toggle">
        <button
          type="button"
          class="theme-button"
          @click="toggleTheme"
          :aria-label="themeLabel"
          :title="themeLabel"
        >
          <span aria-hidden="true">{{ themeIcon }}</span>
        </button>
      </div>

      <div class="photo-frame">
        <img
          src="https://images.unsplash.com/photo-1518791841217-8f162f1e1131?auto=format&fit=crop&w=480&q=80"
          alt="Circular cat portrait"
        />
      </div>

      <div class="copy-block">
        <p class="eyebrow">Hello, I’m</p>
        <h1>David Ketchum</h1>
        <p class="tagline">Senior UX Design Consultant at Slalom</p>
      </div>

      <nav class="link-list" aria-label="Primary links">
        <a
          v-for="link in links"
          :key="link.label"
          :href="link.href"
          class="link-button"
          target="_blank"
          rel="noreferrer noopener"
        >
          {{ link.label }}
        </a>
      </nav>
    </section>
  </main>
</template>

<style scoped>
.page-shell {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 2rem 1rem 3rem;
}

.profile-card {
  width: min(100%, 480px);
  display: grid;
  gap: 1.75rem;
  padding: 2rem 1.75rem 2.5rem;
  border-radius: 32px;
  background: rgba(var(--card-rgb), 0.96);
  border: 1px solid rgba(var(--card-border-rgb), 0.22);
  box-shadow: 0 28px 80px rgba(0, 0, 0, 0.16);
  backdrop-filter: blur(18px);
}

.theme-toggle {
  display: flex;
  justify-content: flex-end;
}

.theme-button {
  border: 1px solid var(--button-border);
  font: inherit;
  font-weight: 700;
  color: var(--text);
  background: var(--button-bg);
  padding: 0.8rem 1rem;
  border-radius: 999px;
  cursor: pointer;
  transition: transform 0.25s ease, background-color 0.25s ease, border-color 0.25s ease;
}

.theme-button:hover {
  transform: translateY(-1px);
  background: var(--button-hover-bg);
}

.photo-frame {
  width: 140px;
  height: 140px;
  margin: 0 auto;
  border-radius: 50%;
  overflow: hidden;
  border: 4px solid rgba(var(--ring-rgb), 0.28);
  box-shadow: 0 24px 40px rgba(0, 0, 0, 0.18);
}

.photo-frame img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.copy-block {
  display: grid;
  gap: 0.8rem;
  text-align: center;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.28em;
  font-size: 0.76rem;
  color: var(--text-muted);
}

h1 {
  margin: 0;
  font-size: clamp(2.1rem, 4vw, 3rem);
  line-height: 1.05;
  color: var(--heading);
}

.tagline {
  max-width: 34rem;
  margin: 0 auto;
  color: var(--text-muted);
  line-height: 1.75;
}

.link-list {
  display: grid;
  gap: 1rem;
}

.link-button {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 56px;
  width: 100%;
  padding: 0 1.5rem;
  color: var(--button-text);
  text-decoration: none;
  font-weight: 700;
  letter-spacing: 0.01em;
  border-radius: 999px;
  background-image: linear-gradient(var(--button-bg), var(--button-bg)), linear-gradient(125deg, var(--accent), var(--accent-alt), var(--accent2));
  background-origin: border-box;
  background-clip: padding-box, border-box;
  background-size: 100% 100%, 220% 100%;
  background-position: center, 0% 0%;
  transition: transform 0.22s ease, background-position 0.8s ease, color 0.2s ease;
  overflow: hidden;
  border: 2px solid transparent;
}

.link-button:hover {
  transform: translateY(-1px);
  background-position: center, 100% 0%;
}

.link-button:active {
  transform: translateY(0);
}
</style>
