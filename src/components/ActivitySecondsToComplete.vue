<script setup>
import { formatSeconds, getTotalActivitySeconds } from '@/functions'
import { isActivityValid } from '@/validators'
import { computed, inject } from 'vue'

const props = defineProps({
  activity: {
    type: Object,
    required: true,
    validator: isActivityValid,
  }
})

const timelineItems = inject('timelineItems') 
const secondsDiff = computed(
  () =>
    getTotalActivitySeconds(props.activity, timelineItems) - props.activity.secondsToComplete
)
const colorClasses = computed(() =>
  secondsDiff.value < 0 ? 'bg-red-100 text-red-600' : 'bg-green-100 text-green-600'
)
const classes = computed(() =>
  `flex items-center rounded bg-purple-100 px-2 font-mono text-xl ${colorClasses.value}`
)



const sign = computed(() => (secondsDiff.value < 0 ? '-' : '+'))

const seconds = computed(() => `${sign.value}${formatSeconds(secondsDiff.value)}`)
</script>
<template>
  <div :class="classes">
    {{ seconds }}
  </div>
</template>