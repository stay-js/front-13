<template>
  <main class="min-h-screen py-20 px-6 max-w-6xl mx-auto flex flex-col gap-12">
    <CreateOption @unshift="unshift" @push="push" @clearAll="clearAll" />

    <CurrentResult
      :count="count"
      :totalVotes="totalVotes"
      :winnerText="winnerText"
      :lastInsert="lastInsert"
    />

    <Options
      :options="options"
      :count="count"
      @addVote="addVote"
      @resetVotes="resetVotes"
      @deleteOption="deleteOption"
    />
  </main>
</template>

<script setup>
import { ref, computed } from 'vue';

import CreateOption from '@components/CreateOption.vue';
import CurrentResult from '@components/CurrentResult.vue';
import Options from '@components/Options.vue';

const options = ref([
  { id: 0, text: 'React', votes: 10 },
  { id: 1, text: 'Vue', votes: 6 },
  { id: 2, text: 'Angular', votes: 3 },
  { id: 3, text: 'Svelte', votes: 8 },
  { id: 4, text: 'Solid', votes: 4 },
]);

const lastInsert = ref('nincs');
const nextId = ref(options.value.length);

const count = computed(() => options.value.length);
const totalVotes = computed(() => options.value.reduce((acc, opt) => acc + opt.votes, 0));

const winnerText = computed(() => {
  if (options.value.length === 0) return 'nincs';

  if (totalVotes.value === 0) return 'még nincs szavazat';

  const maxVotes = Math.max(...options.value.map((opt) => opt.votes));
  const winners = options.value.filter((opt) => opt.votes === maxVotes);

  if (winners.length > 1) return 'holtverseny';

  return winners[0].text;
});

const insertOption = (position, option) => {
  if (option === '') return;

  const newOption = {
    id: nextId.value++,
    text: option,
    votes: 0,
  };

  if (position === 'unshift') {
    options.value.unshift(newOption);
    lastInsert.value = 'eleje';
  } else {
    options.value.push(newOption);
    lastInsert.value = 'vége';
  }
};

const unshift = (option) => insertOption('unshift', option);
const push = (option) => insertOption('push', option);

const addVote = (idx) => options.value[idx].votes++;
const resetVotes = (idx) => (options.value[idx].votes = 0);
const deleteOption = (idx) => options.value.splice(idx, 1);

const clearAll = () => {
  if (confirm('Biztosan törölsz minden opciót?')) {
    options.value = [];
    lastInsert.value = 'nincs';
  }
};
</script>
