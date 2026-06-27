<script setup lang="ts">
import { computed } from 'vue'
import { useTheme } from 'vuetify'
import LinkButton from '@/components/LinkButton.vue'

const theme = useTheme()
const isDark = computed(() => theme.global.name.value === 'dark')

const themeIcon = computed(() => (isDark.value ? 'mdi-weather-sunny' : 'mdi-weather-night'))
const themeLabel = computed(() =>
  isDark.value ? 'Switch to light theme' : 'Switch to dark theme'
)

const toggleTheme = () => {
  theme.global.name.value = isDark.value ? 'light' : 'dark'
}

const links = [
  {
    label: 'Portfolio',
    href: 'https://davidketchum.design',
    icon: 'mdi-briefcase',
  },
  {
    label: 'Dribbble',
    href: 'https://dribbble.com/davidketchum',
    icon: 'mdi-dribbble',
  },
  {
    label: 'LinkedIn',
    href: 'https://linkedin.com/in/david-ketchum',
    icon: 'mdi-linkedin',
  },
  {
    label: 'Email',
    href: 'mailto:david.ketchum@slalom.com',
    icon: 'mdi-email',
  },
]
</script>

<template>
  <v-app>
    <v-main>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center" class="pa-0">
          <v-col cols="12" sm="10" md="8" lg="6">
            <v-card elevation="10" class="pa-8">
              <div class="d-flex justify-end mb-6">
                <v-btn icon variant="tonal" size="small" @click="toggleTheme" :aria-label="themeLabel" :title="themeLabel">
                  <v-icon>{{ themeIcon }}</v-icon>
                </v-btn>
              </div>

              <div class="d-flex justify-center mb-6">
                <v-avatar size="140">
                  <img
                    src="https://images.unsplash.com/photo-1518791841217-8f162f1e1131?auto=format&fit=crop&w=480&q=80"
                    alt="Cat portrait"
                  />
                </v-avatar>
              </div>

              <div class="text-center mb-8">
                <div class="text-overline mb-2">Hello, I’m</div>
                <div class="text-h4 font-weight-bold mb-2">David Ketchum</div>
                <div class="text-subtitle-1">Senior UX Design Consultant at Slalom</div>
              </div>

              <v-row dense>
                <v-col cols="12" v-for="link in links" :key="link.label">
                  <LinkButton :label="link.label" :url="link.href" :icon="link.icon" />
                </v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
