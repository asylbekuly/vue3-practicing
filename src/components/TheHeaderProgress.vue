<script setup>
import BaseIcon from '@/components/BaseIcon.vue'
import { HUNDRED_PERCENT, PAGE_PROGRESS } from '../constants'
import { ICON_CHECK_CIRCLE } from '@/icons'
import { navigate } from '@/router'
import { useTotalProgress } from '@/composables/total-progress'
const { colorClass, percentage } = useTotalProgress()
</script>

<template>
  <a :href="`#${PAGE_PROGRESS}`" @click="navigate(PAGE_PROGRESS)" class="text-sm">
    <div v-if="percentage < HUNDRED_PERCENT" class="flex items-center gap-1">
      <div>
        Progress: <span class="font-mono">{{ percentage }}%</span>
      </div>
      <div :class="`h-3 w-3 rounded-full ${colorClass}`"></div>
    </div>
    <div v-else class="flex items-center gap-1">
      Day complete!
      <BaseIcon :name="ICON_CHECK_CIRCLE" class="h-7 w-7 text-green-500" />
    </div>
  </a>
</template>
