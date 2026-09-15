<script setup lang="ts">
import { computed } from 'vue'
import { cn } from '@/lib/utils'

interface Props {
  variant?: 'default' | 'glass' | 'interactive' | 'glow'
  className?: string
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'default',
  className: '',
})

const variantClasses = computed(() => {
  switch (props.variant) {
    case 'glass':
      return 'bg-[var(--bg-glass)] backdrop-blur-xl border border-[var(--border-color)] shadow-[var(--shadow-card)]'
    case 'interactive':
      return 'bg-[var(--bg-card)] border border-[var(--border-color)] hover:border-[var(--brand-primary)] hover:shadow-xl hover:-translate-y-1 transition-all duration-300'
    case 'glow':
      return 'bg-[var(--bg-card)] border border-[var(--border-color)] relative overflow-hidden group hover:shadow-[var(--shadow-elevated)] transition-all duration-300'
    case 'default':
    default:
      return 'bg-[var(--bg-card)] border border-[var(--border-color)] shadow-[var(--shadow-card)]'
  }
})
</script>

<template>
  <div :class="cn('rounded-2xl p-6 transition-colors', variantClasses, className)">
    <slot />
  </div>
</template>
