<script setup lang="ts">
import { ref, computed } from 'vue'
import {
  Compass,
  Star,
  MapPin,
  Clock,
  ArrowUpRight,
  Heart,
  Sparkles,
} from 'lucide-vue-next'
import Card from '@/components/ui/Card.vue'
import Badge from '@/components/ui/Badge.vue'
import Button from '@/components/ui/Button.vue'
import './destinations.css'

interface Destination {
  id: number
  num: string
  title: string
  location: string
  country: string
  category: 'Trending' | 'Beaches' | 'Mountain' | 'Cultural'
  price: number
  rating: number
  reviews: number
  duration: string
  badge: string
  badgeVariant: 'primary' | 'accent' | 'glass'
  image: string
}

const activeCategory = ref<string>('All')
const favorites = ref<number[]>([1, 4])
const selectedId = ref<number>(1)

const toggleFavorite = (id: number) => {
  if (favorites.value.includes(id)) {
    favorites.value = favorites.value.filter((item) => item !== id)
  } else {
    favorites.value.push(id)
  }
}

const categories = ['All', 'Trending', 'Beaches', 'Mountain', 'Cultural']

const destinations: Destination[] = [
  {
    id: 1,
    num: '01',
    title: 'Kyoto Zen Gardens & Bamboo Groves',
    location: 'Kyoto',
    country: 'Japan',
    category: 'Cultural',
    price: 1350,
    rating: 4.95,
    reviews: 428,
    duration: '7 Days',
    badge: 'AI Curated',
    badgeVariant: 'primary',
    image: 'https://images.unsplash.com/photo-1493976040374-85c8e12f0c0e?auto=format&fit=crop&w=800&q=80',
  },
  {
    id: 2,
    num: '02',
    title: 'Amalfi Coast Cliffside Serenade',
    location: 'Positano',
    country: 'Italy',
    category: 'Beaches',
    price: 1890,
    rating: 4.92,
    reviews: 312,
    duration: '6 Days',
    badge: 'Trending',
    badgeVariant: 'accent',
    image: 'https://images.unsplash.com/photo-1533105079780-92b9be482077?auto=format&fit=crop&w=800&q=80',
  },
  {
    id: 3,
    num: '03',
    title: 'Zermatt Glacier Alpine Trek',
    location: 'Matterhorn',
    country: 'Switzerland',
    category: 'Mountain',
    price: 2150,
    rating: 4.98,
    reviews: 196,
    duration: '8 Days',
    badge: 'Adventure',
    badgeVariant: 'glass',
    image: 'https://images.unsplash.com/photo-1530122037265-a5f1f91d3b99?auto=format&fit=crop&w=800&q=80',
  },
  {
    id: 4,
    num: '04',
    title: 'Santorini Sunset Caldera Villa',
    location: 'Oia',
    country: 'Greece',
    category: 'Beaches',
    price: 1640,
    rating: 4.89,
    reviews: 512,
    duration: '5 Days',
    badge: 'Top Rated',
    badgeVariant: 'accent',
    image: 'https://images.unsplash.com/photo-1570077188670-e3a8d69ac5ff?auto=format&fit=crop&w=800&q=80',
  },
  {
    id: 5,
    num: '05',
    title: 'Reykjavik Northern Lights Expedition',
    location: 'Reykjavik',
    country: 'Iceland',
    category: 'Trending',
    price: 1780,
    rating: 4.93,
    reviews: 284,
    duration: '6 Days',
    badge: 'Rare Experience',
    badgeVariant: 'primary',
    image: 'https://images.unsplash.com/photo-1517411032315-54ef2cb783bb?auto=format&fit=crop&w=800&q=80',
  },
  {
    id: 6,
    num: '06',
    title: 'Banff National Park Emerald Waters',
    location: 'Alberta',
    country: 'Canada',
    category: 'Mountain',
    price: 1420,
    rating: 4.91,
    reviews: 350,
    duration: '7 Days',
    badge: 'Nature Pick',
    badgeVariant: 'glass',
    image: 'https://images.unsplash.com/photo-1503614472-8c93d56e92ce?auto=format&fit=crop&w=800&q=80',
  },
]

const filteredDestinations = computed(() => {
  if (activeCategory.value === 'All') return destinations
  return destinations.filter((dest) => dest.category === activeCategory.value)
})
</script>

<template>
  <section id="destinations" class="destinations-section">
    <div class="destinations-container">
      <!-- Section Header -->
      <div class="destinations-header">
        <div>
          <div class="destinations-tag">
            <Compass class="w-4 h-4" />
            <span>Handpicked Voyages</span>
          </div>
          <h2 class="destinations-title">
            Popular Destinations
          </h2>
          <p class="destinations-subtitle">
            Discover destinations travelers are falling in love with this season, complete with AI-optimized daily schedules.
          </p>
        </div>

        <!-- Filter Pill Tabs -->
        <div class="flex items-center gap-1.5 overflow-x-auto pb-2 md:pb-0">
          <button
            v-for="cat in categories"
            :key="cat"
            :class="[
              'px-4 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all duration-200 cursor-pointer',
              activeCategory === cat
                ? 'bg-[var(--brand-primary)] text-white shadow-md'
                : 'bg-[var(--bg-secondary)] text-[var(--text-secondary)] hover:text-[var(--text-primary)] hover:bg-[var(--bg-card)] border border-[var(--border-color)]',
            ]"
            @click="activeCategory = cat"
          >
            {{ cat }}
          </button>
        </div>
      </div>

      <!-- Destination Card Grid with 3D Hover & Glass Styling -->
      <div class="destinations-grid">
        <Card
          v-for="dest in filteredDestinations"
          :key="dest.id"
          variant="interactive"
          class="destination-card p-0 overflow-hidden group flex flex-col justify-between"
        >
          <!-- Image Header -->
          <div class="destination-card-image-box">
            <img
              :src="dest.image"
              :alt="dest.title"
              loading="lazy"
              class="destination-card-image"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-black/75 via-black/20 to-transparent" />

            <!-- Floating Top Badges -->
            <div class="absolute top-3.5 left-3.5 flex items-center gap-2">
              <Badge :variant="dest.badgeVariant">
                {{ dest.badge }}
              </Badge>
              <span class="text-[10px] font-extrabold px-2 py-0.5 rounded-full bg-black/50 text-white backdrop-blur-md">
                #{{ dest.num }}
              </span>
            </div>

            <!-- Favorite Button -->
            <button
              type="button"
              class="absolute top-3.5 right-3.5 w-9 h-9 rounded-full bg-black/40 backdrop-blur-md border border-white/20 flex items-center justify-center text-white hover:scale-110 active:scale-95 transition-all duration-200 cursor-pointer"
              :aria-label="'Favorite ' + dest.title"
              @click.stop="toggleFavorite(dest.id)"
            >
              <Heart
                :class="[
                  'w-4 h-4 transition-colors',
                  favorites.includes(dest.id) ? 'fill-rose-500 text-rose-500' : 'text-white',
                ]"
              />
            </button>

            <!-- Bottom Location Tag -->
            <div class="absolute bottom-3 left-4 right-4 flex items-center justify-between text-white text-xs">
              <span class="flex items-center gap-1 font-semibold drop-shadow">
                <MapPin class="w-3.5 h-3.5 text-sky-400" />
                {{ dest.location }}, {{ dest.country }}
              </span>
              <span class="flex items-center gap-1 font-semibold drop-shadow">
                <Clock class="w-3.5 h-3.5 text-teal-300" />
                {{ dest.duration }}
              </span>
            </div>
          </div>

          <!-- Card Content Body -->
          <div class="p-5 flex flex-col flex-grow justify-between gap-4">
            <div>
              <div class="flex items-center justify-between gap-2 mb-1.5">
                <div class="flex items-center gap-1 text-xs font-bold text-amber-500">
                  <Star class="w-3.5 h-3.5 fill-amber-400 text-amber-400" />
                  <span>{{ dest.rating }}</span>
                  <span class="text-[var(--text-muted)] font-normal">({{ dest.reviews }})</span>
                </div>
                <span class="text-xs text-[var(--text-muted)] font-medium">Hotel & Transit included</span>
              </div>
              <h3 class="text-lg font-bold text-[var(--text-primary)] line-clamp-1 group-hover:text-[var(--brand-primary)] transition-colors">
                {{ dest.title }}
              </h3>
            </div>

            <!-- Footer: Price & CTA -->
            <div class="pt-3 border-t border-[var(--border-color)] flex items-center justify-between">
              <div>
                <span class="text-xs text-[var(--text-muted)]">Starting from</span>
                <div class="text-xl font-extrabold text-[var(--text-primary)]">
                  ${{ dest.price }}
                  <span class="text-xs font-normal text-[var(--text-muted)]">/ pax</span>
                </div>
              </div>

              <a
                href="#planner"
                class="inline-flex items-center gap-1 text-xs font-bold px-3 py-2 rounded-xl bg-[var(--bg-secondary)] hover:bg-[var(--brand-primary)] hover:text-white text-[var(--text-primary)] transition-all cursor-pointer border border-[var(--border-color)]"
              >
                <span>Book Itinerary</span>
                <ArrowUpRight class="w-3.5 h-3.5" />
              </a>
            </div>
          </div>
        </Card>
      </div>
    </div>
  </section>
</template>
