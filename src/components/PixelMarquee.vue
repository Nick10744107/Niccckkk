<template>
  <div class="border-y-2 border-ink overflow-hidden" :class="bg" aria-hidden="true">
    <div class="flex w-max animate-marquee py-2.5">
      <span
        v-for="n in 2"
        :key="n"
        class="font-pixel text-sm whitespace-nowrap pr-2"
        :class="textColor"
      >
        {{ line }}
      </span>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  items: { type: Array, required: true },
  variant: { type: String, default: "snake" }, // snake | apple | ink
});

const line = computed(() => props.items.map((t) => `${t}  ▸  `).join(""));

const bg = computed(
  () =>
    ({ snake: "bg-snake", apple: "bg-apple", ink: "bg-ink" })[props.variant]
);
const textColor = computed(() =>
  props.variant === "ink" ? "text-phosphor" : "text-white"
);
</script>
