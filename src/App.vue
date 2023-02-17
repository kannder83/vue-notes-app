<script setup>
import { ref } from "vue";
const showModal = ref(false);
const newNote = ref("");
const errorMessage = ref("");
const notes = ref([]);

let colorIndex = 0;

const selectBgColor = () => {
  const bgColors = [
    "bg-[#888888]",
    "bg-[#8899AA]",
    "bg-[#bbccdd]",
    "bg-[#eeff00]",
    "bg-[#778899]",
  ];

  let indexBgColor = "";

  if (colorIndex > bgColors.length - 1) {
    colorIndex = 0;
  }

  indexBgColor = bgColors[colorIndex];

  colorIndex++;

  return indexBgColor;
};

const addNote = () => {
  if (newNote.value.length < 10) {
    errorMessage.value =
      "* You must create a note with more than 10 characters.";
    return;
  }
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: selectBgColor(),
  });
  showModal.value = false;
  newNote.value = "";
  errorMessage.value = "";
};
</script>

<template>
  <main class="w-full min-h-screen">
    <div
      v-show="showModal"
      class="absolute w-full min-h-screen flex justify-center items-center bg-black/70 z-10"
    >
      <div class="w-3/4 p-8 flex flex-col rounded-xl bg-white">
        <textarea
          class="p-3 text-3xl rounded-xl text-gray-600"
          v-model.trim="newNote"
          name="note"
          id="note"
          cols="30"
          rows="6"
        ></textarea>
        <p class="text-red-600 text-2xl" v-show="errorMessage">
          {{ errorMessage }}
        </p>
        <button
          @click="addNote()"
          class="w-full px-3 py-5 mt-4 border-none rounded-xl text-white bg-violet-300 text-xl cursor-pointer hover:bg-violet-400 hover:shadow-sm transition-all duration-200"
        >
          Add Note
        </button>
        <button
          @click="showModal = false"
          class="w-full px-3 py-5 mt-4 border-none rounded-xl text-white bg-red-300 text-xl cursor-pointer hover:bg-red-400 hover:shadow-sm transition-all duration-200"
        >
          Close
        </button>
      </div>
    </div>
    <div class="mx-auto container p-3">
      <header class="m-12 flex justify-between items-center">
        <h1 class="text-7xl font-bold">Notes</h1>
        <button
          @click="showModal = true"
          class="flex justify-center items-center border-none p-3 h-12 w-12 text-xl cursor-pointer bg-black/80 rounded-full text-white font-extrabold"
        >
          +
        </button>
      </header>
      <div class="flex flex-wrap">
        <article
          v-for="note in notes"
          :key="note.id"
          class="w-56 h-56 p-3 mr-5 mb-5 flex flex-col justify-between rounded-xl shadow-md"
          :class="`${note.backgroundColor}`"
        >
          <p>
            {{ note.text }}
          </p>
          <p class="text-xs font-bold">
            {{ note.date.toLocaleDateString("en-US") }}
          </p>
        </article>
      </div>
    </div>
  </main>
</template>
