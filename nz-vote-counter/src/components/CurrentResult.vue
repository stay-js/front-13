<template>
  <section class="bg-zinc-900 text-white p-8 rounded-lg flex flex-col gap-4">
    <div class="grid md:grid-cols-3 gap-6">
      <div class="bg-zinc-950 p-4 rounded-lg flex flex-col gap-2">
        <h3 class="text-lg font-semibold text-zinc-200">Opciók száma</h3>
        <p class="text-3xl font-bold text-blue-600">{{ count }}</p>
      </div>

      <div class="bg-zinc-950 p-4 rounded-lg flex flex-col gap-2">
        <h3 class="text-lg font-semibold text-zinc-200">Összes szavazat</h3>
        <p class="text-3xl font-bold text-purple-600">{{ totalVotes }}</p>
      </div>

      <div class="bg-zinc-950 p-4 rounded-lg flex flex-col gap-2">
        <h3 class="text-lg font-semibold text-zinc-200">Vezető opció</h3>
        <p class="text-2xl font-bold text-green-600">{{ winnerText }}</p>
      </div>
    </div>

    <h5 class="text-lg">
      <span class="font-semibold text-zinc-300">Utolsó beszúrás iránya: </span>
      <span class="text-indigo-600 font-bold">{{ lastInsert }}</span>
    </h5>
  </section>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps(['count', 'totalVotes', 'winnerText', 'lastInsert']);
</script>
