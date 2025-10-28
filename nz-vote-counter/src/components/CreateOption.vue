<template>
  <section class="bg-zinc-900 text-white p-8 rounded-lg flex flex-col gap-4">
    <h2 class="text-2xl font-bold">Új Opció Hozzáadása</h2>

    <input
      v-model.trim="newOption"
      type="text"
      placeholder="Adjon hozzá új opciót..."
      class="outline rounded-md px-4 py-2 outline-zinc-700 focus:ring-4 focus:ring-zinc-800 bg-zinc-950"
      @keyup.enter="push"
    />

    <div class="flex gap-3 flex-wrap">
      <button
        @click="unshift"
        class="px-4 py-2 bg-green-500 hover:bg-green-500/80 text-sm text-white cursor-pointer font-semibold rounded-md transition-colors"
      >
        Beszúrás az elejére
      </button>

      <button
        @click="push"
        class="px-4 py-2 bg-blue-500 hover:bg-blue-500/80 text-sm text-white cursor-pointer font-semibold rounded-md transition-colors"
      >
        Beszúrás a végére
      </button>

      <button
        @click="clearAll"
        class="px-4 py-2 bg-red-500 hover:bg-red-500/80 text-sm text-white cursor-pointer font-semibold rounded-md transition-colors"
      >
        Összes Törlése
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const newOption = ref('');

const emits = defineEmits(['unshift', 'push', 'clearAll']);

const unshift = () => {
  emits('unshift', newOption.value);
  newOption.value = '';
};

const push = () => {
  emits('push', newOption.value);
  newOption.value = '';
};

const clearAll = () => emits('clearAll');
</script>
