<script setup>
import { ref } from "vue";
const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date(),
  });
  console.log(notes);
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
          v-model="newNote"
          name="note"
          id="note"
          cols="30"
          rows="6"
        ></textarea>
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
          class="w-56 h-56 p-3 mr-5 mb-5 flex flex-col justify-between bg-yellow-200 rounded-xl shadow-md"
        >
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit
            repellendus, totam numquam eligendi debitis necessitatibus!
          </p>
          <p class="text-xs font-bold">12/feb/2023</p>
        </article>
      </div>
    </div>
  </main>
</template>
