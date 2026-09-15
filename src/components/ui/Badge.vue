<script setup lang="ts">
import { computed } from 'vue'
import { cn } from '@/lib/utils'

interface Props {
  variant?: 'primary' | 'secondary' | 'accent' | 'outline' | 'glass'
  className?: string
  dot?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'glass',
  className: '',
  dot: false,
})

const variantClasses = computed(() => {
  switch (props.variant) {
    case 'primary':
      return 'bg-sky-500/10 text-sky-600 dark:text-sky-400 border-sky-500/20'
    case 'accent':
      return 'bg-amber-500/10 text-amber-600 dark:text-amber-400 border-amber-500/20'
    case 'outline':
      return 'bg-transparent text-[var(--text-secondary)] border-[var(--border-color)]'
    case 'secondary':
      return 'bg-[var(--bg-secondary)] text-[var(--text-secondary)] border-[var(--border-color)]'
    case 'glass':
    default:
      return 'bg-[var(--bg-glass)] text-[var(--text-primary)] border-[var(--border-color)] shadow-sm backdrop-blur-md'
  }
})
</script>

<template>
  <span
    :class="
      cn(
        'inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-semibold border tracking-wide select-none',
        variantClasses,
        className
      )
    "
  >
    <span
      v-if="dot"
      class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse shrink-0"
    />
    <slot />
  </span>
</template>
