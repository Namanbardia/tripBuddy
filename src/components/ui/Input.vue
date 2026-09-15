<script setup lang="ts">
import { cn } from '@/lib/utils'

interface Props {
  modelValue?: string | number
  type?: string
  placeholder?: string
  disabled?: boolean
  className?: string
  label?: string
  error?: string
}

defineProps<Props>()

defineEmits<{
  (e: 'update:modelValue', value: string): void
}>()
</script>

<template>
  <div class="flex flex-col gap-1.5 w-full text-left">
    <label
      v-if="label"
      class="text-xs font-semibold text-[var(--text-secondary)] uppercase tracking-wider"
    >
      {{ label }}
    </label>
    <div class="relative flex items-center">
      <div v-if="$slots.icon" class="absolute left-3.5 text-[var(--text-muted)] pointer-events-none flex items-center">
        <slot name="icon" />
      </div>
      <input
        :type="type || 'text'"
        :value="modelValue"
        :placeholder="placeholder"
        :disabled="disabled"
        :class="
          cn(
            'w-full rounded-xl bg-[var(--bg-glass-input)] text-[var(--text-primary)] border border-[var(--border-color)] placeholder:text-[var(--text-muted)] text-sm px-4 py-2.5 transition-all duration-200 outline-none focus:border-[var(--brand-primary)] focus:ring-2 focus:ring-[var(--ring-focus)] disabled:opacity-50 disabled:cursor-not-allowed',
            $slots.icon ? 'pl-10' : '',
            error ? 'border-red-500 focus:ring-red-500/20' : '',
            className
          )
        "
        @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
      />
    </div>
    <span v-if="error" class="text-xs text-red-500 mt-0.5 font-medium">{{ error }}</span>
  </div>
</template>
