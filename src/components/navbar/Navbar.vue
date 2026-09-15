<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import {
  Compass,
  Sun,
  Moon,
  Menu,
  X,
  LogIn,
  MapPin,
  Sparkles,
  ShieldCheck,
} from 'lucide-vue-next'
import { useTheme } from '@/composables/useTheme'
import Button from '@/components/ui/Button.vue'
import './navbar.css'

defineEmits<{
  (e: 'open-login'): void
}>()

const { isDark, toggleTheme } = useTheme()
const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'Destinations', href: '#destinations', icon: MapPin },
  { name: 'AI Planner', href: '#planner', icon: Sparkles },
  { name: 'Why TripBuddy', href: '#features', icon: ShieldCheck },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const scrollToSection = (e: MouseEvent, href: string) => {
  e.preventDefault()
  isMobileMenuOpen.value = false
  const target = document.querySelector(href)
  if (target) {
    const navbarHeight = 80
    const elementPosition = target.getBoundingClientRect().top
    const offsetPosition = elementPosition + window.pageYOffset - navbarHeight

    window.scrollTo({
      top: offsetPosition,
      behavior: 'smooth',
    })
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header
    :class="[
      'navbar-header',
      isScrolled ? 'scrolled' : 'unscrolled',
    ]"
  >
    <div class="navbar-container">
      <!-- Brand Logo -->
      <a href="#" class="navbar-brand" @click.prevent="scrollToTop">
        <div class="navbar-brand-icon">
          <Compass class="w-5 h-5" />
        </div>
        <div class="flex flex-col">
          <span class="navbar-brand-title">
            Trip<span>Buddy</span>
          </span>
          <span class="navbar-brand-subtitle">
            Travel Smart
          </span>
        </div>
      </a>

      <!-- 2-3 Navigation Redirect Buttons -->
      <nav class="navbar-nav">
        <a
          v-for="link in navLinks"
          :key="link.name"
          :href="link.href"
          class="navbar-nav-link"
          @click="scrollToSection($event, link.href)"
        >
          <component :is="link.icon" class="w-3.5 h-3.5 opacity-75" />
          {{ link.name }}
        </a>
      </nav>

      <!-- Right Action Corner: Theme Toggle & Login Button -->
      <div class="navbar-actions">
        <!-- Light / Dark Mode Toggle with CSS Variables -->
        <button
          type="button"
          class="theme-toggle-btn p-2 rounded-xl border border-[var(--border-color)] bg-[var(--bg-secondary)] hover:bg-[var(--bg-surface)] text-[var(--text-primary)] transition-all cursor-pointer flex items-center justify-center hover:border-[var(--brand-primary)]"
          aria-label="Toggle color mode"
          @click="toggleTheme"
        >
          <Sun
            v-if="isDark"
            class="w-4 h-4 text-amber-400 transition-transform rotate-0 hover:rotate-90 duration-300"
          />
          <Moon
            v-else
            class="w-4 h-4 text-slate-700 transition-transform rotate-0 hover:-rotate-12 duration-300"
          />
        </button>

        <!-- Login Button in Right Corner -->
        <Button
          variant="shimmer"
          size="md"
          class="hidden sm:inline-flex shadow-sm"
          @click="$emit('open-login')"
        >
          <LogIn class="w-3.5 h-3.5 mr-1" />
          <span>Log in</span>
        </Button>

        <!-- Mobile Menu Toggle Button -->
        <button
          type="button"
          class="p-2 rounded-xl border border-[var(--border-color)] text-[var(--text-primary)] md:hidden cursor-pointer bg-[var(--bg-secondary)]"
          aria-label="Toggle Mobile Navigation"
          @click="isMobileMenuOpen = !isMobileMenuOpen"
        >
          <X v-if="isMobileMenuOpen" class="w-5 h-5" />
          <Menu v-else class="w-5 h-5" />
        </button>
      </div>
    </div>

    <!-- Mobile Navigation Drawer -->
    <div v-if="isMobileMenuOpen" class="navbar-mobile-drawer">
      <a
        v-for="link in navLinks"
        :key="link.name"
        :href="link.href"
        class="flex items-center gap-2.5 px-3 py-2.5 rounded-xl text-sm font-semibold text-[var(--text-primary)] hover:bg-[var(--bg-secondary)]"
        @click="scrollToSection($event, link.href)"
      >
        <component :is="link.icon" class="w-4 h-4 text-[var(--brand-primary)]" />
        {{ link.name }}
      </a>
      <div class="pt-2 border-t border-[var(--border-color)]">
        <Button
          variant="primary"
          size="md"
          class="w-full justify-center"
          @click="
            isMobileMenuOpen = false;
            $emit('open-login');
          "
        >
          <LogIn class="w-4 h-4 mr-2" />
          <span>Log in</span>
        </Button>
      </div>
    </div>
  </header>
</template>
