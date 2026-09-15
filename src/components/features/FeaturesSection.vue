<script setup lang="ts">
import {
  BrainCircuit,
  Wallet2,
  Headphones,
  CloudSun,
  ShieldCheck,
  CheckCircle,
  Quote,
  Star,
} from 'lucide-vue-next'
import './features.css'

const features = [
  {
    icon: BrainCircuit,
    title: 'Adaptive AI Engine',
    desc: 'Calibrates daily schedules to your personal pacing and stamina so you never feel rushed.',
    color: 'bg-gradient-to-tr from-sky-500 to-blue-600',
  },
  {
    icon: Wallet2,
    title: 'Transparent Budgeting',
    desc: 'Real-time multi-currency expense forecasts. Lock in excursions with zero surprise fees.',
    color: 'bg-gradient-to-tr from-teal-500 to-emerald-600',
  },
  {
    icon: Headphones,
    title: '24/7 On-Ground Guides',
    desc: 'Connected to verified local guides and emergency response teams across 120+ destinations.',
    color: 'bg-gradient-to-tr from-indigo-500 to-violet-600',
  },
  {
    icon: CloudSun,
    title: 'Weather & Crowd Sync',
    desc: 'Dynamic rerouting when rain strikes or landmarks hit peak tourist congestion.',
    color: 'bg-gradient-to-tr from-amber-500 to-orange-600',
  },
]
</script>

<template>
  <section id="features" class="features-section">
    <div class="features-container">
      <!-- Section Header -->
      <div class="features-header">
        <div class="features-tag">
          <ShieldCheck class="w-3.5 h-3.5 text-sky-500" />
          <span>The TripBuddy Standard</span>
        </div>
        <h2 class="features-title">
          Built for travelers who want <br />
          <span class="bg-gradient-to-r from-sky-500 via-teal-400 to-indigo-500 bg-clip-text text-transparent">
            frictionless discovery
          </span>
        </h2>
        <p class="text-[var(--text-secondary)] text-base">
          Say goodbye to juggling 14 browser tabs, messy spreadsheets, and outdated blog recommendations.
        </p>
      </div>

      <!-- Features Grid -->
      <div class="features-grid">
        <div
          v-for="(feat, idx) in features"
          :key="idx"
          class="features-card"
        >
          <div>
            <div :class="['features-icon-box', feat.color]">
              <component :is="feat.icon" class="w-6 h-6" />
            </div>
            <h3 class="text-lg font-bold text-[var(--text-primary)] mb-2">
              {{ feat.title }}
            </h3>
            <p class="text-sm text-[var(--text-secondary)] leading-relaxed">
              {{ feat.desc }}
            </p>
          </div>

          <div class="mt-6 pt-4 border-t border-[var(--border-color)] flex items-center gap-1.5 text-xs font-semibold text-[var(--brand-primary)]">
            <CheckCircle class="w-4 h-4 text-emerald-500" />
            <span>Included in all accounts</span>
          </div>
        </div>
      </div>

      <!-- Testimonial Card -->
      <div class="mt-14 max-w-4xl mx-auto rounded-2xl p-8 bg-[var(--bg-surface)] border border-[var(--border-color)] shadow-xl relative overflow-hidden">
        <Quote class="absolute -bottom-4 -right-4 w-32 h-32 text-[var(--border-color)]/25 pointer-events-none" />
        <div class="flex flex-col sm:flex-row items-center gap-6 relative z-10">
          <img
            src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=200&q=80"
            alt="Elena Rostova"
            class="w-20 h-20 rounded-2xl object-cover ring-4 ring-sky-500/20 shrink-0 shadow-md"
          />
          <div class="text-center sm:text-left space-y-2">
            <div class="flex justify-center sm:justify-start items-center gap-1 text-amber-400">
              <Star v-for="i in 5" :key="i" class="w-4 h-4 fill-amber-400" />
            </div>
            <p class="text-[var(--text-primary)] font-medium text-base sm:text-lg italic">
              “TripBuddy made our 2-week Japan road trip effortless. When typhoons caused rail delays, the AI automatically rearranged our temple reservations and found us an indoor sake tasting.”
            </p>
            <div class="text-xs text-[var(--text-muted)] font-medium">
              <strong class="text-[var(--text-primary)] font-semibold">Elena Rostova</strong> — Solo & Couple Explorer, visited 34 countries
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
