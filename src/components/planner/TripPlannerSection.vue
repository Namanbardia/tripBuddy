<script setup lang="ts">
import { ref, computed } from 'vue'
import {
  Sparkles,
  Palmtree,
  Mountain,
  Utensils,
  Landmark,
  HeartHandshake,
  CheckCircle2,
  Calendar,
  ArrowRight,
} from 'lucide-vue-next'
import Button from '@/components/ui/Button.vue'
import './planner.css'

const vibes = [
  { id: 'relax', name: 'Relax & Chill', icon: Palmtree, desc: 'Scenic beaches, spas & slow living' },
  { id: 'adventure', name: 'Thrill & Nature', icon: Mountain, desc: 'Hiking, climbing & wild safaris' },
  { id: 'foodie', name: 'Gourmet & Street', icon: Utensils, desc: 'Michelin tasting & night markets' },
  { id: 'culture', name: 'Heritage & Art', icon: Landmark, desc: 'Museums, castles & ancient lore' },
  { id: 'romantic', name: 'Couples Retreat', icon: HeartHandshake, desc: 'Private sunsets & candlelit dinners' },
]

const budgetTiers = [
  { id: 'budget', label: 'Smart Saver', range: '$50 - $100 / day' },
  { id: 'balanced', label: 'Balanced Comfort', range: '$150 - $250 / day' },
  { id: 'luxury', label: 'Boutique & Luxury', range: '$400+ / day' },
]

const durations = ['3 Days', '7 Days', '12 Days']

const selectedVibe = ref('adventure')
const selectedBudget = ref('balanced')
const selectedDuration = ref('7 Days')
const isGenerating = ref(false)

const currentVibeData = computed(() => {
  return vibes.find((v) => v.id === selectedVibe.value) || vibes[0]!
})

const itineraryHighlights = computed(() => {
  switch (selectedVibe.value) {
    case 'relax':
      return [
        { day: 'Day 1-2', title: 'Sunset Catamaran & Hydrotherapy Spa', tag: 'Wellness' },
        { day: 'Day 3-4', title: 'Private Island Beach Hop & Coconut Groove', tag: 'Leisure' },
        { day: 'Day 5-7', title: 'Eco-Resort Stargazing & Chef Tasting Table', tag: 'Gastronomy' },
      ]
    case 'foodie':
      return [
        { day: 'Day 1-2', title: 'Hidden Alley Noodle Trails & Craft Breweries', tag: 'Street Food' },
        { day: 'Day 3-4', title: 'Vineyard Cellar Masterclass & Truffle Foraging', tag: 'Wine & Dine' },
        { day: 'Day 5-7', title: 'Michelin Star Chef Collaborative Dinner', tag: 'Fine Dining' },
      ]
    case 'culture':
      return [
        { day: 'Day 1-2', title: 'Private Access Museum & Ancient Citadel Tour', tag: 'History' },
        { day: 'Day 3-4', title: 'Old Quarter Artisan Ceramic & Tea Workshop', tag: 'Tradition' },
        { day: 'Day 5-7', title: 'Cathedral Acoustic Concert & Twilight Walk', tag: 'Music' },
      ]
    case 'romantic':
      return [
        { day: 'Day 1-2', title: 'Cliffside Infinity Pool & Welcome Champagne', tag: 'Intimate' },
        { day: 'Day 3-4', title: 'Hot Air Balloon Sunrise & Picnic in Olive Groves', tag: 'Adventure' },
        { day: 'Day 5-7', title: 'Private Yacht Cruise & Candlelight Beach Gala', tag: 'Luxury' },
      ]
    case 'adventure':
    default:
      return [
        { day: 'Day 1-2', title: 'Alpine Ridge Via Ferrata & Basecamp Prep', tag: 'High Elevation' },
        { day: 'Day 3-4', title: 'Whitewater River Rafting & Forest Zip-line', tag: 'Adrenaline' },
        { day: 'Day 5-7', title: 'Glacier Blue Ice Cave Exploration & Campfire', tag: 'Expedition' },
      ]
  }
})

const handleRegenerate = () => {
  isGenerating.value = true
  setTimeout(() => {
    isGenerating.value = false
  }, 350)
}
</script>

<template>
  <section id="planner" class="planner-section">
    <div class="planner-container">
      <!-- Section Header -->
      <div class="planner-header">
        <div class="planner-tag">
          <Sparkles class="w-3.5 h-3.5" />
          <span>Interactive AI Studio</span>
        </div>
        <h2 class="planner-title">
          Design your dream route in seconds
        </h2>
        <p class="planner-subtitle">
          Choose your travel style, pace, and spending plan. Our AI engine builds an adaptive day-by-day itinerary tailored to you.
        </p>
      </div>

      <!-- Planner Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
        <!-- Controls Column -->
        <div class="lg:col-span-7 space-y-6">
          <!-- Step 1: Vibe Selection -->
          <div class="planner-card">
            <div class="flex items-center gap-2 mb-4">
              <span class="planner-step-badge">1</span>
              <h3 class="font-bold text-[var(--text-primary)] text-base">Select Your Travel Vibe</h3>
            </div>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
              <div
                v-for="vibe in vibes"
                :key="vibe.id"
                :class="[
                  'p-3.5 rounded-xl border transition-all cursor-pointer flex items-start gap-3',
                  selectedVibe === vibe.id
                    ? 'border-[var(--brand-primary)] bg-sky-500/10 shadow-sm'
                    : 'border-[var(--border-color)] bg-[var(--bg-surface)] hover:border-[var(--brand-primary)]/50',
                ]"
                @click="selectedVibe = vibe.id; handleRegenerate()"
              >
                <div
                  :class="[
                    'w-9 h-9 rounded-lg flex items-center justify-center shrink-0',
                    selectedVibe === vibe.id
                      ? 'bg-[var(--brand-primary)] text-white'
                      : 'bg-[var(--bg-secondary)] text-[var(--text-secondary)]',
                  ]"
                >
                  <component :is="vibe.icon" class="w-4 h-4" />
                </div>
                <div>
                  <div class="font-semibold text-sm text-[var(--text-primary)]">{{ vibe.name }}</div>
                  <div class="text-xs text-[var(--text-muted)] mt-0.5">{{ vibe.desc }}</div>
                </div>
              </div>
            </div>
          </div>

          <!-- Step 2: Budget & Duration -->
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
            <!-- Budget Tier -->
            <div class="planner-card">
              <div class="flex items-center gap-2 mb-4">
                <span class="planner-step-badge">2</span>
                <h3 class="font-bold text-[var(--text-primary)] text-base">Daily Budget</h3>
              </div>
              <div class="space-y-2">
                <div
                  v-for="tier in budgetTiers"
                  :key="tier.id"
                  :class="[
                    'p-3 rounded-xl border flex items-center justify-between cursor-pointer transition-all',
                    selectedBudget === tier.id
                      ? 'border-[var(--brand-primary)] bg-sky-500/10'
                      : 'border-[var(--border-color)] bg-[var(--bg-surface)] hover:border-[var(--brand-primary)]/40',
                  ]"
                  @click="selectedBudget = tier.id"
                >
                  <div class="text-sm font-semibold text-[var(--text-primary)]">{{ tier.label }}</div>
                  <div class="text-xs font-mono font-bold text-[var(--brand-primary)]">{{ tier.range }}</div>
                </div>
              </div>
            </div>

            <!-- Duration -->
            <div class="planner-card">
              <div class="flex items-center gap-2 mb-4">
                <span class="planner-step-badge">3</span>
                <h3 class="font-bold text-[var(--text-primary)] text-base">Duration</h3>
              </div>
              <div class="grid grid-cols-3 gap-2">
                <button
                  v-for="dur in durations"
                  :key="dur"
                  :class="[
                    'py-3 rounded-xl border text-xs font-bold text-center cursor-pointer transition-all',
                    selectedDuration === dur
                      ? 'border-[var(--brand-primary)] bg-[var(--brand-primary)] text-white shadow-md'
                      : 'border-[var(--border-color)] bg-[var(--bg-surface)] text-[var(--text-secondary)] hover:border-[var(--brand-primary)]/50',
                  ]"
                  @click="selectedDuration = dur"
                >
                  {{ dur }}
                </button>
              </div>
              <div class="mt-4 p-3 rounded-xl bg-[var(--bg-secondary)] border border-[var(--border-color)] text-xs text-[var(--text-muted)] flex items-center gap-2">
                <Calendar class="w-4 h-4 text-[var(--brand-primary)] shrink-0" />
                <span>Flexible departures available weekly</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Live Preview Output Column -->
        <div class="lg:col-span-5">
          <div
            :class="[
              'rounded-2xl p-6 sticky top-28 border-2 border-sky-500/30 bg-[var(--bg-surface)] shadow-2xl transition-opacity duration-300',
              isGenerating ? 'opacity-60' : 'opacity-100',
            ]"
          >
            <!-- Preview Header -->
            <div class="flex items-center justify-between pb-4 border-b border-[var(--border-color)]">
              <div class="flex items-center gap-2">
                <div class="w-8 h-8 rounded-lg bg-gradient-to-tr from-sky-500 to-teal-500 flex items-center justify-center text-white">
                  <Sparkles class="w-4 h-4" />
                </div>
                <div>
                  <div class="text-xs font-bold uppercase tracking-wider text-[var(--brand-primary)]">AI Generated Plan</div>
                  <h4 class="text-base font-extrabold text-[var(--text-primary)]">
                    {{ currentVibeData.name }} Experience
                  </h4>
                </div>
              </div>
              <span class="px-2.5 py-1 rounded-full text-xs font-bold bg-sky-500/10 text-[var(--brand-primary)]">
                {{ selectedDuration }}
              </span>
            </div>

            <!-- Timeline items -->
            <div class="py-5 space-y-4">
              <div
                v-for="(item, idx) in itineraryHighlights"
                :key="idx"
                class="flex items-start gap-3 relative"
              >
                <div class="flex flex-col items-center">
                  <div class="w-5 h-5 rounded-full bg-sky-500/20 border-2 border-sky-500 flex items-center justify-center text-sky-500 text-[10px] font-bold">
                    {{ idx + 1 }}
                  </div>
                  <div v-if="idx < itineraryHighlights.length - 1" class="w-0.5 h-10 bg-[var(--border-color)] mt-1" />
                </div>

                <div class="flex-1 bg-[var(--bg-secondary)] p-3 rounded-xl border border-[var(--border-color)]">
                  <div class="flex items-center justify-between mb-1">
                    <span class="text-xs font-bold text-[var(--brand-primary)]">{{ item.day }}</span>
                    <span class="text-[10px] font-semibold px-2 py-0.5 rounded-md bg-[var(--bg-surface)] text-[var(--text-muted)]">
                      {{ item.tag }}
                    </span>
                  </div>
                  <div class="text-xs font-semibold text-[var(--text-primary)]">{{ item.title }}</div>
                </div>
              </div>
            </div>

            <!-- Summary & Actions -->
            <div class="pt-4 border-t border-[var(--border-color)] space-y-3">
              <div class="flex items-center justify-between text-xs text-[var(--text-muted)]">
                <span class="flex items-center gap-1">
                  <CheckCircle2 class="w-3.5 h-3.5 text-emerald-500" /> Auto-synced flight alerts
                </span>
                <span class="font-bold text-[var(--text-primary)]">Route #TB-{{ selectedVibe.slice(0, 3).toUpperCase() }}</span>
              </div>

              <Button
                variant="shimmer"
                size="lg"
                class="w-full justify-center shadow-md font-bold"
              >
                <span>Customize & Lock Itinerary</span>
                <ArrowRight class="w-4 h-4 ml-2" />
              </Button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
