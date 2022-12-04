<script setup>
import { computed } from 'vue'
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'

const now = useNow()
const christmas = new Date('12/25/2022 00:00:00')
const diffTime = computed(() => christmas.getTime() - now.value.getTime())

const second = 1000
const minute = second * 60
const hour = minute * 60
const day = hour * 24

const diffDays = computed(() => Math.floor(diffTime.value / day))
const diffHours = computed(() => Math.floor((diffTime.value % day) / hour))
const diffMinutes = computed(() => Math.floor((diffTime.value % hour) / minute))
const diffSeconds = computed(() => Math.floor((diffTime.value % minute) / second))

</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="diffDays" />
          <CountdownSegment label="hours" :number="diffHours" />
          <CountdownSegment label="minutes" :number="diffMinutes" />
          <CountdownSegment label="seconds" :number="diffSeconds" />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
