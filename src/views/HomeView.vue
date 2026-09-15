<script setup lang="ts">
import { ref } from 'vue'
import Navbar from '@/components/navbar/Navbar.vue'
import HeroSection from '@/components/hero/HeroSection.vue'
import DestinationsSection from '@/components/destinations/DestinationsSection.vue'
import TripPlannerSection from '@/components/planner/TripPlannerSection.vue'
import FeaturesSection from '@/components/features/FeaturesSection.vue'
import FooterSection from '@/components/footer/FooterSection.vue'
import LoginModal from '@/components/login-modal/LoginModal.vue'

const isLoginModalOpen = ref(false)

const openLoginModal = () => {
  isLoginModalOpen.value = true
}

const closeLoginModal = () => {
  isLoginModalOpen.value = false
}
</script>

<template>
  <div class="min-h-screen flex flex-col bg-[var(--bg-primary)] text-[var(--text-primary)] transition-colors duration-200 selection:bg-sky-500 selection:text-white">
    <!-- Fixed Navbar on Top with Section Redirects, Theme Toggle and Login Button -->
    <Navbar @open-login="openLoginModal" />

    <!-- Main Content Area -->
    <main class="flex-grow">
      <!-- Hero Section -->
      <HeroSection />

      <!-- Section 1: Destinations (#destinations) -->
      <DestinationsSection />

      <!-- Section 2: AI Trip Planner (#planner) -->
      <TripPlannerSection />

      <!-- Section 3: Why TripBuddy (#features) -->
      <FeaturesSection />
    </main>

    <!-- Footer Section -->
    <FooterSection />

    <!-- Login / Sign Up Modal -->
    <LoginModal :is-open="isLoginModalOpen" @close="closeLoginModal" />
  </div>
</template>
