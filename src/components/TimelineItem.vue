<script setup>
import BaseSelect from '@/components/BaseSelect.vue'
import {
  isTimelineItemValid,
  isActivityValid,
  isValidHour,
} from '@/validators'
import TimelineHour from './TimelineHour.vue'
import { NULLABLE_ACTIVITY } from '@/constants'
import TimelineStopWatch from './TimelineStopWatch.vue'
import { inject } from 'vue'

defineProps({
  timelineItem: {
    type: Object,
    required: true,
    validator: isTimelineItemValid,
  }
})
const emit = defineEmits({
  selectActivity: isActivityValid,
  scrollToHour: isValidHour,
})
const activities = inject('activities')
const activitySelectOptions = inject('activitySelectOptions')

function findActivityById(id) {
  return activities.find((activity) => activity.id === id) || NULLABLE_ACTIVITY
}
function selectActivity(id) {
  emit('selectActivity', id ? findActivityById(id) : NULLABLE_ACTIVITY)
}
</script>
<template>
  <li class="relative flex flex-col gap-2 border-t border-gray-200 py-10 px-4">
    <TimelineHour
      :hour="timelineItem.hour"
      @click.prevent="emit('scrollToHour', timelineItem.hour)"
    />
    <BaseSelect
      :selected="timelineItem.activityId"
      :options="activitySelectOptions"
      placeholder="Rest"
      @select="selectActivity"
    />
    <TimelineStopWatch :timelineItem="timelineItem"></TimelineStopWatch>
  </li>
</template>  