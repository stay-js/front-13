<template>
  <section class="flex flex-col gap-4">
    <h2 class="text-2xl font-bold">Szavazás</h2>

    <div v-if="count === 0" class="p-8 text-center bg-zinc-900 rounded-lg">Nincs még opció.</div>

    <div v-else class="grid sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <div
        v-for="(opt, idx) in options"
        :key="opt.id"
        class="bg-zinc-900 rounded-lg overflow-hidden"
      >
        <div
          class="bg-gradient-to-r from-indigo-500 to-blue-500 p-4 text-white font-semibold text-lg"
        >
          {{ opt.text }}
        </div>

        <div class="flex flex-col gap-4 p-4">
          <div class="text-center flex flex-col gap-2">
            <p class="text-zinc-200 font-medium">Szavazatok</p>
            <p class="text-5xl font-bold text-indigo-600">{{ opt.votes }}</p>
          </div>

          <div class="flex flex-col gap-2 px-4">
            <button
              @click="addVote(idx)"
              class="px-4 py-2 bg-green-500 hover:bg-green-500/80 text-sm text-white cursor-pointer font-semibold rounded-md transition-colors"
            >
              Szavazok
            </button>

            <button
              @click="resetVotes(idx)"
              class="px-4 py-2 bg-yellow-500 hover:bg-yellow-500/80 text-sm text-white cursor-pointer font-semibold rounded-md transition-colors"
            >
              Nullázás
            </button>

            <button
              @click="deleteOption(idx)"
              class="px-4 py-2 bg-red-500 hover:bg-red-500/80 text-sm text-white cursor-pointer font-semibold rounded-md transition-colors"
            >
              Törlés
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps(['options', 'count']);
const emits = defineEmits(['addVote', 'resetVotes', 'deleteOption']);

const addVote = (idx) => emits('addVote', idx);
const resetVotes = (idx) => emits('resetVotes', idx);
const deleteOption = (idx) => emits('deleteOption', idx);
</script>
