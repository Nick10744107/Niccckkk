<template>
  <section id="contact" class="py-32 px-6 bg-black relative overflow-hidden">
    <!-- background glow -->
    <div
      class="absolute bottom-0 left-1/2 -translate-x-1/2 w-125 h-75 bg-violet-600/10 rounded-full blur-[100px] pointer-events-none"
    ></div>

    <div class="relative max-w-xl mx-auto">
      <div class="mb-12 text-center">
        <p class="text-violet-400 text-xs tracking-widest uppercase mb-3">
          Get in touch
        </p>
        <h2 class="text-4xl font-bold text-white mb-3">聯絡我</h2>
        <p class="text-white/40">有任何合作機會或想法，歡迎來信！</p>
      </div>

      <form @submit.prevent="handleSubmit" class="space-y-5">
        <div>
          <label
            class="block text-xs font-medium text-white/50 tracking-wider uppercase mb-2"
            >姓名</label
          >
          <input
            v-model="form.name"
            type="text"
            placeholder="Your name"
            class="w-full px-5 py-3.5 bg-white/5 border border-white/10 rounded-xl text-white placeholder-white/20 focus:outline-none focus:border-violet-500/60 focus:bg-white/[0.07] transition-all duration-300"
          />
        </div>
        <div>
          <label
            class="block text-xs font-medium text-white/50 tracking-wider uppercase mb-2"
            >Email</label
          >
          <input
            v-model="form.email"
            type="email"
            placeholder="your@email.com"
            class="w-full px-5 py-3.5 bg-white/5 border border-white/10 rounded-xl text-white placeholder-white/20 focus:outline-none focus:border-violet-500/60 focus:bg-white/[0.07] transition-all duration-300"
          />
        </div>
        <div>
          <label
            class="block text-xs font-medium text-white/50 tracking-wider uppercase mb-2"
            >訊息</label
          >
          <textarea
            v-model="form.message"
            rows="5"
            placeholder="Tell me about your project..."
            class="w-full px-5 py-3.5 bg-white/5 border border-white/10 rounded-xl text-white placeholder-white/20 focus:outline-none focus:border-violet-500/60 focus:bg-white/[0.07] transition-all duration-300 resize-none"
          />
        </div>
        <button
          type="submit"
          class="w-full py-4 bg-linear-to-r from-violet-600 to-pink-600 text-white rounded-xl font-semibold hover:opacity-90 hover:scale-[1.02] transition-all duration-300 tracking-wide"
        >
          送出訊息 →
        </button>
      </form>

      <div
        v-if="sent"
        class="mt-8 text-center p-5 rounded-xl border border-violet-500/30 bg-violet-500/10 text-violet-300"
      >
        訊息已送出！我會盡快回覆你。
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
