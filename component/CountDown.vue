<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const props = defineProps({
  date: {
    type: String,
    required: true,
  },
  label: {
    type: String,
    required: false,
    default: '',
  },
});

const now = ref(new Date());
let interval = null;

onMounted(() => {
  interval = setInterval(() => {
    now.value = new Date();
  }, 1000);
});

onUnmounted(() => {
  clearInterval(interval);
});

const targetDate = computed(() => new Date(props.date));

const timeLeft = computed(() => {
  const diff = targetDate.value - now.value;

  if (diff <= 0) {
    return { expired: true, days: 0, hours: 0, minutes: 0, seconds: 0 };
  }

  const days = Math.floor(diff / (1000 * 60 * 60 * 24));
  const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
  const seconds = Math.floor((diff % (1000 * 60)) / 1000);

  return { expired: false, days, hours, minutes, seconds };
});

const pad = (n) => String(n).padStart(2, '0');
</script>

<template>
  <div class="flex flex-col items-center gap-3">
    <p v-if="label" class="text-sm uppercase tracking-widest text-[#999]">{{ label }}</p>

    <div v-if="timeLeft.expired" class="text-2xl font-bold text-red-500">
      Date has passed!
    </div>

    <div v-else class="flex items-center gap-4">
      <div class="flex flex-col items-center">
        <span class="text-4xl font-bold tabular-nums text-[#333]">{{ timeLeft.days }}</span>
        <span class="text-xs uppercase tracking-widest text-[#999] mt-1">Days</span>
      </div>

      <span class="text-3xl font-bold text-[#ccc] mb-4">:</span>

      <div class="flex flex-col items-center">
        <span class="text-4xl font-bold tabular-nums text-[#333]">{{ pad(timeLeft.hours) }}</span>
        <span class="text-xs uppercase tracking-widest text-[#999] mt-1">Hours</span>
      </div>

      <span class="text-3xl font-bold text-[#ccc] mb-4">:</span>

      <div class="flex flex-col items-center">
        <span class="text-4xl font-bold tabular-nums text-[#333]">{{ pad(timeLeft.minutes) }}</span>
        <span class="text-xs uppercase tracking-widest text-[#999] mt-1">Minutes</span>
      </div>

      <span class="text-3xl font-bold text-[#ccc] mb-4">:</span>

      <div class="flex flex-col items-center">
        <span class="text-4xl font-bold tabular-nums text-[#333]">{{ pad(timeLeft.seconds) }}</span>
        <span class="text-xs uppercase tracking-widest text-[#999] mt-1">Seconds</span>
      </div>
    </div>
  </div>
</template>