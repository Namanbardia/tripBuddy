<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import {
  X,
  Mail,
  Lock,
  Compass,
  ArrowRight,
  Eye,
  EyeOff,
  CheckCircle2,
} from 'lucide-vue-next'
import Button from '@/components/ui/Button.vue'
import './login-modal.css'

interface Props {
  isOpen: boolean
}

defineProps<Props>()

const emit = defineEmits<{
  (e: 'close'): void
}>()

const activeTab = ref<'login' | 'signup'>('login')
const email = ref('')
const password = ref('')
const name = ref('')
const showPassword = ref(false)
const rememberMe = ref(true)
const isSubmitted = ref(false)

const handleKeyDown = (e: KeyboardEvent) => {
  if (e.key === 'Escape') {
    emit('close')
  }
}

const handleSubmit = () => {
  isSubmitted.value = true
  setTimeout(() => {
    isSubmitted.value = false
    emit('close')
  }, 1200)
}

onMounted(() => {
  window.addEventListener('keydown', handleKeyDown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeyDown)
})
</script>

<template>
  <Teleport to="body">
    <div v-if="isOpen" class="modal-backdrop">
      <!-- Modal Container -->
      <div class="modal-card">
        <div class="modal-glow" />

        <!-- Close Button -->
        <button
          type="button"
          class="modal-close-btn"
          aria-label="Close dialog"
          @click="$emit('close')"
        >
          <X class="w-5 h-5" />
        </button>

        <!-- Brand Header -->
        <div class="text-center mb-6">
          <div
            class="w-12 h-12 mx-auto mb-3 rounded-2xl bg-gradient-to-tr from-sky-500 to-teal-400 flex items-center justify-center text-white shadow-lg shadow-sky-500/25"
          >
            <Compass class="w-6 h-6" />
          </div>
          <h3 class="text-2xl font-extrabold text-[var(--text-primary)] tracking-tight">
            {{ activeTab === 'login' ? 'Welcome Back' : 'Join TripBuddy' }}
          </h3>
          <p class="text-xs text-[var(--text-muted)] mt-1">
            {{
              activeTab === 'login'
                ? 'Access your saved itineraries, bookings, and custom routes'
                : 'Unlock personalized travel guides, member perks, and discounts'
            }}
          </p>
        </div>

        <!-- Tab Toggle -->
        <div class="modal-tab-bar">
          <button
            type="button"
            :class="['modal-tab-btn', activeTab === 'login' ? 'active' : 'inactive']"
            @click="activeTab = 'login'"
          >
            Log In
          </button>
          <button
            type="button"
            :class="['modal-tab-btn', activeTab === 'signup' ? 'active' : 'inactive']"
            @click="activeTab = 'signup'"
          >
            Sign Up
          </button>
        </div>

        <!-- Success Toast State -->
        <div
          v-if="isSubmitted"
          class="p-6 rounded-2xl bg-emerald-500/10 border border-emerald-500/30 text-center space-y-2"
        >
          <CheckCircle2 class="w-10 h-10 text-emerald-500 mx-auto" />
          <h4 class="font-bold text-emerald-600 dark:text-emerald-400">Authenticated!</h4>
          <p class="text-xs text-[var(--text-secondary)]">Opening your travel companion...</p>
        </div>

        <!-- Form Body -->
        <form v-else class="space-y-4" @submit.prevent="handleSubmit">
          <div v-if="activeTab === 'signup'" class="flex flex-col gap-1.5 text-left">
            <label class="text-xs font-semibold text-[var(--text-secondary)] uppercase tracking-wider">
              Full Name
            </label>
            <input
              v-model="name"
              type="text"
              placeholder="Jane Doe"
              required
              class="w-full rounded-xl bg-[var(--bg-glass-input)] text-[var(--text-primary)] border border-[var(--border-color)] placeholder:text-[var(--text-muted)] text-sm px-4 py-2.5 outline-none focus:border-[var(--brand-primary)]"
            />
          </div>

          <div class="flex flex-col gap-1.5 text-left">
            <label class="text-xs font-semibold text-[var(--text-secondary)] uppercase tracking-wider">
              Email Address
            </label>
            <div class="relative flex items-center">
              <Mail class="absolute left-3.5 w-4 h-4 text-[var(--text-muted)] pointer-events-none" />
              <input
                v-model="email"
                type="email"
                placeholder="you@example.com"
                required
                class="w-full rounded-xl bg-[var(--bg-glass-input)] text-[var(--text-primary)] border border-[var(--border-color)] placeholder:text-[var(--text-muted)] text-sm pl-10 pr-4 py-2.5 outline-none focus:border-[var(--brand-primary)]"
              />
            </div>
          </div>

          <div class="flex flex-col gap-1.5 text-left">
            <div class="flex items-center justify-between">
              <label class="text-xs font-semibold text-[var(--text-secondary)] uppercase tracking-wider">
                Password
              </label>
              <a
                v-if="activeTab === 'login'"
                href="#"
                class="text-xs font-medium text-[var(--brand-primary)] hover:underline"
                @click.prevent
              >
                Forgot?
              </a>
            </div>

            <div class="relative flex items-center">
              <Lock class="absolute left-3.5 w-4 h-4 text-[var(--text-muted)] pointer-events-none" />
              <input
                v-model="password"
                :type="showPassword ? 'text' : 'password'"
                placeholder="••••••••"
                required
                class="w-full rounded-xl bg-[var(--bg-glass-input)] text-[var(--text-primary)] border border-[var(--border-color)] placeholder:text-[var(--text-muted)] text-sm pl-10 pr-10 py-2.5 outline-none focus:border-[var(--brand-primary)]"
              />
              <button
                type="button"
                class="absolute right-3.5 text-[var(--text-muted)] hover:text-[var(--text-primary)] cursor-pointer"
                @click="showPassword = !showPassword"
              >
                <EyeOff v-if="showPassword" class="w-4 h-4" />
                <Eye v-else class="w-4 h-4" />
              </button>
            </div>
          </div>

          <div class="flex items-center justify-between text-xs pt-1">
            <label class="flex items-center gap-2 cursor-pointer select-none text-[var(--text-secondary)]">
              <input
                v-model="rememberMe"
                type="checkbox"
                class="rounded border-[var(--border-color)] text-[var(--brand-primary)]"
              />
              <span>Remember this device</span>
            </label>
          </div>

          <!-- Submit Button -->
          <Button
            variant="shimmer"
            size="lg"
            type="submit"
            class="w-full justify-center font-bold shadow-md mt-2"
          >
            <span>{{ activeTab === 'login' ? 'Log In' : 'Create Free Account' }}</span>
            <ArrowRight class="w-4 h-4 ml-2" />
          </Button>
        </form>
      </div>
    </div>
  </Teleport>
</template>
