<template>
  <section id="contact" class="py-28 px-6 bg-shell dot-grid">
    <div class="max-w-xl mx-auto">
      <div class="mb-12 text-center" data-reveal>
        <p class="font-pixel text-apple text-sm mb-3 animate-blink-px">
          CONTINUE?
        </p>
        <h2 class="font-pixel text-4xl text-ink mb-3">聯絡我</h2>
        <p class="text-ink/60">有任何合作機會或想法,歡迎來信!</p>
      </div>

      <form
        @submit.prevent="handleSubmit"
        class="pixel-box bg-white p-6 sm:p-8 space-y-5"
        data-reveal
      >
        <div>
          <Label for="contact-name" class="font-pixel text-sm text-ink mb-2"
            >姓名</Label
          >
          <Input
            id="contact-name"
            v-model="form.name"
            type="text"
            placeholder="Your name"
            class="h-auto px-4 py-3 bg-shell border-2 text-base text-ink placeholder:text-ink/30 focus-visible:ring-snake/40 focus-visible:border-snake transition-colors duration-150"
          />
        </div>
        <div>
          <Label for="contact-email" class="font-pixel text-sm text-ink mb-2"
            >EMAIL</Label
          >
          <Input
            id="contact-email"
            v-model="form.email"
            type="email"
            placeholder="your@email.com"
            class="h-auto px-4 py-3 bg-shell border-2 text-base text-ink placeholder:text-ink/30 focus-visible:ring-snake/40 focus-visible:border-snake transition-colors duration-150"
          />
        </div>
        <div>
          <Label for="contact-message" class="font-pixel text-sm text-ink mb-2"
            >訊息</Label
          >
          <Textarea
            id="contact-message"
            v-model="form.message"
            :rows="5"
            placeholder="Tell me about your project..."
            class="px-4 py-3 bg-shell border-2 text-base text-ink placeholder:text-ink/30 focus-visible:ring-snake/40 focus-visible:border-snake transition-colors duration-150 resize-none"
          />
        </div>
        <Button
          type="submit"
          class="pixel-box w-full h-auto py-3.5 bg-snake text-white font-pixel text-base hover:-translate-x-0.5 hover:-translate-y-0.5 hover:shadow-[6px_6px_0_0_#0b2440] hover:bg-snake transition-all duration-150"
        >
          送出訊息 ▸
        </Button>
      </form>

      <div
        v-if="sent"
        class="pixel-box mt-8 text-center p-5 bg-snake text-white font-pixel text-sm"
      >
        訊息已送出!我會盡快回覆你。
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

const form = ref({ name: "", email: "", message: "" });
const sent = ref(false);

function handleSubmit() {
  console.log("送出", form.value);
  sent.value = true;
  form.value = { name: "", email: "", message: "" };
}
</script>
