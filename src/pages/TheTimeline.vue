<script setup>
import TimelineItem from '@/components/TimelineItem.vue'
import { onActivated } from 'vue'

import { scrollToCurrentHour, timelineItems, timelineItemRefs } from '@/timeline-items'

onActivated(scrollToCurrentHour)
</script>

<template>
  <div class="mt-8">
    <ul>
      <TimelineItem
        v-for="timelineItem in timelineItems"
        :key="timelineItem.hour"
        :timeline-item="timelineItem"
        ref="timelineItemRefs"
      />
    </ul>
  </div>
</template>
