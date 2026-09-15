<script setup lang="ts">
import { ref } from 'vue'
import {
  MapPin,
  Calendar,
  Users,
  Search,
  Sparkles,
  ArrowRight,
  Star,
  ShieldCheck,
  TrendingUp,
} from 'lucide-vue-next'
import Button from '@/components/ui/Button.vue'
import './hero.css'

const searchDestination = ref('')
const searchDate = ref('')
const searchGuests = ref('2 Travelers')

const trendingPills = ['Tokyo, Japan', 'Amalfi Coast, Italy', 'Bali, Indonesia', 'Swiss Alps']

const onSearch = () => {
  const target = document.querySelector('#destinations')
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
</script>

<template>
  <section class="hero-section">
    <!-- Ambient glowing backgrounds -->
    <div class="hero-glow-1" />
    <div class="hero-glow-2" />

    <div class="hero-container">
      <!-- Pill Badge -->
      <div class="hero-badge-container">
        <div class="hero-badge">
          <Sparkles class="w-4 h-4 text-sky-500" />
          <span>TripBuddy 3.0 Live • AI Curated Journeys</span>
          <ArrowRight class="w-3.5 h-3.5 opacity-60" />
        </div>
      </div>

      <!-- Main Headline & Subtitle -->
      <div class="hero-headline-wrapper">
        <h1 class="hero-title">
          Explore the world, <br />
          <span class="hero-title-gradient">
            curated for your soul.
          </span>
        </h1>
        <p class="hero-subtitle">
          Craft unforgettable custom itineraries in seconds. Compare top hidden gems, budget effortlessly, and explore with verified local insider guides.
        </p>
      </div>

      <!-- Quick Search Widget -->
      <div class="hero-search-card">
        <div class="hero-search-grid">
          <!-- Destination Field -->
          <div class="hero-search-field">
            <MapPin class="w-5 h-5 text-[var(--brand-primary)] shrink-0" />
            <div class="w-full text-left">
              <div class="hero-search-label">Where to?</div>
              <input
                v-model="searchDestination"
                type="text"
                placeholder="e.g. Kyoto, Japan"
                class="hero-search-input"
              />
            </div>
          </div>

          <!-- Date Field -->
          <div class="hero-search-field">
            <Calendar class="w-5 h-5 text-[var(--brand-primary)] shrink-0" />
            <div class="w-full text-left">
              <div class="hero-search-label">When?</div>
              <input
                v-model="searchDate"
                type="text"
                placeholder="Oct 12 - Oct 20"
                class="hero-search-input"
              />
            </div>
          </div>

          <!-- Guests Field -->
          <div class="hero-search-field">
            <Users class="w-5 h-5 text-[var(--brand-primary)] shrink-0" />
            <div class="w-full text-left">
              <div class="hero-search-label">Who?</div>
              <select
                v-model="searchGuests"
                class="hero-search-input cursor-pointer"
              >
                <option value="1 Solo Traveler" class="text-slate-900">1 Solo Traveler</option>
                <option value="2 Travelers" class="text-slate-900">2 Travelers (Couple)</option>
                <option value="3-5 Travelers" class="text-slate-900">3-5 (Family / Group)</option>
                <option value="6+ Travelers" class="text-slate-900">6+ (Large Crew)</option>
              </select>
            </div>
          </div>

          <!-- Search Action Button -->
          <Button
            variant="shimmer"
            size="lg"
            class="w-full h-full min-h-[52px] rounded-xl flex items-center justify-center font-bold text-white shadow-lg"
            @click="onSearch"
          >
            <Search class="w-4 h-4 mr-2" />
            <span>Find Trips</span>
          </Button>
        </div>

        <!-- Trending quick tags -->
        <div class="mt-4 pt-3 border-t border-[var(--border-color)] flex flex-wrap items-center gap-2 text-xs text-[var(--text-muted)]">
          <span class="flex items-center gap-1 font-bold text-[var(--text-secondary)]">
            <TrendingUp class="w-3.5 h-3.5 text-amber-500" /> Popular:
          </span>
          <button
            v-for="tag in trendingPills"
            :key="tag"
            class="px-2.5 py-1 rounded-lg bg-[var(--bg-secondary)] hover:bg-[var(--bg-card)] text-[var(--text-secondary)] hover:text-[var(--brand-primary)] border border-[var(--border-color)] transition-colors cursor-pointer"
            @click="searchDestination = tag"
          >
            {{ tag }}
          </button>
        </div>
      </div>

      <!-- Trust Metrics / Stats Bar -->
      <div class="hero-stats-grid">
        <div class="hero-stat-card">
          <div class="hero-stat-icon bg-sky-500/10 text-sky-500 font-bold">
            <Star class="w-4 h-4 fill-sky-500" />
          </div>
          <div>
            <div class="text-base font-bold text-[var(--text-primary)]">4.9 / 5.0</div>
            <div class="text-xs text-[var(--text-muted)]">Over 18k Reviews</div>
          </div>
        </div>

        <div class="hero-stat-card">
          <div class="hero-stat-icon bg-emerald-500/10 text-emerald-500 font-bold">
            <ShieldCheck class="w-4 h-4" />
          </div>
          <div>
            <div class="text-base font-bold text-[var(--text-primary)]">100%</div>
            <div class="text-xs text-[var(--text-muted)]">Verified Hosts</div>
          </div>
        </div>

        <div class="hero-stat-card">
          <div class="hero-stat-icon bg-indigo-500/10 text-indigo-500 font-bold">
            <Users class="w-4 h-4" />
          </div>
          <div>
            <div class="text-base font-bold text-[var(--text-primary)]">50,000+</div>
            <div class="text-xs text-[var(--text-muted)]">Happy Voyagers</div>
          </div>
        </div>

        <div class="hero-stat-card">
          <div class="hero-stat-icon bg-amber-500/10 text-amber-500 font-bold">
            <MapPin class="w-4 h-4" />
          </div>
          <div>
            <div class="text-base font-bold text-[var(--text-primary)]">120+</div>
            <div class="text-xs text-[var(--text-muted)]">Countries Covered</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
