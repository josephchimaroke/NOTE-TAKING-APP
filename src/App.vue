<template>
  <div class="overlay" v-if="isModalOpen">
    <div class="modal">
      <textarea
        v-model.trim="note"
        name="note"
        id="note"
        cols="30"
        rows="10"
      ></textarea>

      <button @click="addNote">Add Note</button>
      <button @click="closeModel">Close</button>
    </div>
  </div>
  <main>
    <div class="container">
      <header class="head">
        <button @click="openModel">+</button>
        <h1>Add New Note</h1>
      </header>
      <div class="cards-container">
        <div class="card" v-for="note in notes" :key="note.id">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("US") }}</p>
        </div>
        <!-- <div class="card">
          <p class="main-text">Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo et sapiente at doloremque nesciunt ratione molestias sit nisi eveniet iure nulla.</p>
          <p class="date">02/02/2023</p>
        </div>
        <div class="card">
          <p class="main-text">Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo et sapiente at doloremque nesciunt ratione molestias sit nisi eveniet iure nulla.</p>
          <p class="date">02/02/2023</p>
        </div>
        <div class="card">
          <p class="main-text">Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo et sapiente at doloremque nesciunt ratione molestias sit nisi eveniet iure nulla.</p>
          <p class="date">02/02/2023</p>
        </div> -->
      </div>
    </div>
    <footer>
      <div class="container">
        <p>Design by Joseph</p>
      </div>
    </footer>
  </main>
</template>
<script setup="this api replaced by slot-scope in 2.5.0+">
import { ref } from "vue";
const isModalOpen = ref(false);
const note = ref("");
const notes = ref([]);

function openModel() {
  isModalOpen.value = true;
}
function closeModel() {
  isModalOpen.value = false;
}
function addNote() {
  const newNote = {
    text: note.value,
    id: Math.random() * 10000000,
    date: new Date(),
  };
  notes.value.push(newNote);
  console.log(note.value);
  note.value = "";
  isModalOpen.value = false;
}
</script>
<style scoped>
main {
  min-height: 100vh;
  color: #6ab6dc;
  background: #6ab6dc;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.container {
  margin-top: 50px;
  width: min(1100px, 100%);
  margin-left: auto;
  margin-right: auto;
}
.head {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  background-color: white;
  width: 55%;
  height: 15rem;
  border: 2px solid transparent;
  border-radius: 1rem;
}


header button {
  border-color: #6ab6dc;
  background-color: #fff;
  color: #6ab6dc;
  border-radius: 50px;
  padding: 30px;
 border-style: dashed;
  cursor: pointer;
  transition: all 0.2s ease;
}

header button:hover {
  animation: b 1s infinite linear;
}

header button:active {
  box-shadow: 0 0 2px 2px rgb(25, 24, 24) !important;
}

@keyframes b {
  0% {
    box-shadow: 0 0 3px 3px rgba(4, 194, 252, 0.5);
  }
  25% {
    box-shadow: 0 0 5px 5px rgba(7, 238, 200, 0.587)
  }
  50% {
    box-shadow: 0 0 10px 10px rgba(14, 203, 203, 0.5);
  }
  75% {
    box-shadow: 0 0 5px 5px rgba(26, 111, 163, 0.5);
  }
  100% {
    box-shadow: 0 0 3px 3px rgba(17, 111, 139, 0.5);
  }
}

.cards-container {
  display: grid;
  gap: 1rem;
  /* grid-template-columns: repeat(auto-fill, minmax(min(25rem,100%), 1fr)); */
  grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
  width: 100%;
  margin-top: 2rem;
}

.card {
  background-color: white;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 2rem;
  height: 15rem;
  border-radius: 1rem;
}

.card p {
  color: #000;
  font-size: 1.5rem;
  font-weight: 400;
}

.card .date {
  font-size: 1.2rem;
  font-style: italic;
}

footer {
  background: rgba(0, 0, 0, 0.767);
  color: #fff;
  padding-block: 1rem;
  margin-top: 4rem;
}

.overlay {
  position: fixed;
  /* inset: 0; */
  width: 20%;
  margin: 15rem 50rem;
  height: 60%;
  background: rgba(3, 125, 190, 0.853);
  z-index: 5;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  width: min(95rem, 100% - 2rem);
  background: #fff;
  border-radius: 2rem;
  padding: 8rem;
  box-shadow: 0 0 5px 5px rgba(0, 0, 0, 0.341);
}

.modal textarea {
  border-radius: 5px;
  resize: none;
  outline: none;
  width: 20rem;
  font-size: 1.8rem;
}
.main-text{
  width: 100%;
  word-wrap: break-word;
}
.modal button {
  border-radius: 5px;
  outline: none;
  border: none;
  padding: 1rem;
  font-size: 1.7rem;
  font-weight: 600;
  cursor: pointer;
  color: #fff;
  box-shadow: 0 0 3px 3px rgba(0, 0, 0, 0.5);
  transition: all 0.2s ease-in-out;
  margin: 0.5rem 0;
}

.modal button:nth-of-type(1) {
  background: blue;
}

.modal button:nth-of-type(2) {
  background: #6ab6dc;
}

.modal button:active {
  box-shadow: 0 0 1px 1px rgba(0, 0, 0, 0.5);
}
</style>
