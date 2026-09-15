<script setup lang="ts">
import { ref } from 'vue'
import {
  Compass,
  Mail,
  Send,
  CheckCircle2,
  Globe2,
  Heart,
} from 'lucide-vue-next'
import Button from '@/components/ui/Button.vue'
import './footer.css'

const email = ref('')
const subscribed = ref(false)

const handleSubscribe = () => {
  if (email.value) {
    subscribed.value = true
    setTimeout(() => {
      email.value = ''
    }, 2000)
  }
}
</script>

<template>
  <footer class="footer-section">
    <div class="footer-container">
      <div class="footer-grid">
        <!-- Brand Info -->
        <div class="space-y-4">
          <div class="flex items-center gap-2.5">
            <div
              class="w-9 h-9 rounded-xl bg-gradient-to-tr from-sky-500 to-teal-400 flex items-center justify-center text-white shadow-md shadow-sky-500/20"
            >
              <Compass class="w-5 h-5" />
            </div>
            <span class="text-xl font-bold tracking-tight text-[var(--text-primary)]">
              Trip<span class="text-[var(--brand-primary)]">Buddy</span>
            </span>
          </div>
          <p class="text-sm text-[var(--text-secondary)] max-w-sm leading-relaxed">
            Your personal AI travel companion. Designing hyper-personalized itineraries, connecting you to authentic local cultures, and simplifying world exploration.
          </p>

          <!-- Newsletter Form -->
          <div class="pt-2">
            <div class="text-xs font-bold uppercase tracking-wider text-[var(--text-primary)] mb-2">
              Secret Deals & Hidden Gems
            </div>
            <form v-if="!subscribed" class="flex items-center gap-2 max-w-sm" @submit.prevent="handleSubscribe">
              <div class="relative flex-1">
                <Mail class="absolute left-3 top-1/2 -translate-y-1/2 w-4 h-4 text-[var(--text-muted)]" />
                <input
                  v-model="email"
                  type="email"
                  placeholder="Enter your email"
                  required
                  class="w-full pl-9 pr-3 py-2 rounded-xl bg-[var(--bg-glass-input)] text-xs text-[var(--text-primary)] border border-[var(--border-color)] outline-none focus:border-[var(--brand-primary)]"
                />
              </div>
              <Button
                variant="primary"
                size="sm"
                type="submit"
                class="shrink-0"
              >
                <Send class="w-3.5 h-3.5" />
              </Button>
            </form>
            <div v-else class="flex items-center gap-2 text-xs font-semibold text-emerald-500">
              <CheckCircle2 class="w-4 h-4" /> You're on the insider list!
            </div>
          </div>
        </div>

        <!-- Links Column 1 -->
        <div>
          <h4 class="footer-column-title">Destinations</h4>
          <ul class="footer-link-list">
            <li><a href="#destinations">Tokyo & Kyoto</a></li>
            <li><a href="#destinations">Amalfi Coast</a></li>
            <li><a href="#destinations">Swiss Alps</a></li>
            <li><a href="#destinations">Santorini Islands</a></li>
            <li><a href="#destinations">Iceland Glaciers</a></li>
          </ul>
        </div>

        <!-- Links Column 2 -->
        <div>
          <h4 class="footer-column-title">AI Travel Studio</h4>
          <ul class="footer-link-list">
            <li><a href="#planner">Custom Itinerary</a></li>
            <li><a href="#planner">Budget Estimator</a></li>
            <li><a href="#planner">Flight Radar</a></li>
            <li><a href="#features">Local Buddy Network</a></li>
            <li><a href="#features">Safety Index 2026</a></li>
          </ul>
        </div>

        <!-- Links Column 3 -->
        <div>
          <h4 class="footer-column-title">Company</h4>
          <ul class="footer-link-list">
            <li><a href="#">About TripBuddy</a></li>
            <li><a href="#">Press & Media</a></li>
            <li><a href="#">Careers</a></li>
            <li><a href="#">Privacy Policy</a></li>
            <li><a href="#">Terms of Service</a></li>
          </ul>
        </div>
      </div>

      <!-- Bottom Bar -->
      <div class="footer-bottom">
        <div class="flex items-center gap-1">
          <span>&copy; 2026 TripBuddy Inc. Crafted with</span>
          <Heart class="w-3.5 h-3.5 fill-rose-500 text-rose-500 inline" />
          <span>for curious wanderers worldwide.</span>
        </div>
        <div class="flex items-center gap-4">
          <span class="flex items-center gap-1">
            <Globe2 class="w-3.5 h-3.5" /> English (US) • USD ($)
          </span>
        </div>
      </div>
    </div>
  </footer>
</template>
