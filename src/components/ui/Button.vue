<script setup lang="ts">
import { computed } from 'vue'
import { cn } from '@/lib/utils'

interface Props {
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost' | 'shimmer'
  size?: 'sm' | 'md' | 'lg' | 'icon'
  as?: string
  className?: string
  disabled?: boolean
  type?: 'button' | 'submit' | 'reset'
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'primary',
  size: 'md',
  as: 'button',
  className: '',
  disabled: false,
  type: 'button',
})

defineEmits<{
  (e: 'click', event: MouseEvent): void
}>()

const baseClasses =
  'inline-flex items-center justify-center font-medium transition-all duration-200 select-none cursor-pointer disabled:opacity-50 disabled:cursor-not-allowed focus:outline-none focus-visible:ring-2 focus-visible:ring-[var(--brand-primary)]'

const sizeClasses = computed(() => {
  switch (props.size) {
    case 'sm':
      return 'text-xs px-3 py-1.5 rounded-lg gap-1.5'
    case 'lg':
      return 'text-base px-6 py-3 rounded-2xl gap-2.5 font-semibold'
    case 'icon':
      return 'w-10 h-10 rounded-xl p-0 shrink-0'
    case 'md':
    default:
      return 'text-sm px-4 py-2 rounded-xl gap-2'
  }
})

const variantClasses = computed(() => {
  switch (props.variant) {
    case 'secondary':
      return 'bg-[var(--bg-secondary)] text-[var(--text-primary)] hover:bg-[var(--bg-surface)] border border-[var(--border-color)] shadow-sm'
    case 'outline':
      return 'bg-transparent text-[var(--text-primary)] border border-[var(--border-color)] hover:border-[var(--brand-primary)] hover:bg-[var(--bg-secondary)]'
    case 'ghost':
      return 'bg-transparent text-[var(--text-secondary)] hover:text-[var(--text-primary)] hover:bg-[var(--bg-secondary)]'
    case 'shimmer':
      return 'relative overflow-hidden bg-gradient-to-r from-sky-500 via-indigo-500 to-teal-500 text-white shadow-lg hover:shadow-cyan-500/25 active:scale-[0.98]'
    case 'primary':
    default:
      return 'bg-[var(--brand-primary)] hover:bg-[var(--brand-primary-hover)] text-white shadow-md hover:shadow-lg active:scale-[0.98]'
  }
})
</script>

<template>
  <component
    :is="as"
    :type="as === 'button' ? type : undefined"
    :disabled="disabled"
    :class="cn(baseClasses, sizeClasses, variantClasses, className)"
    @click="$emit('click', $event)"
  >
    <slot />
  </component>
</template>
