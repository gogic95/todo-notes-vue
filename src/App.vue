<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Note</button>
        <button @click="showModal=false" class="close">x</button>
      </div>
    </div>
    <div class="container"> 
      <header>
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
      </header>
      <div class="cards-container">
        <div 
          v-for="note in notesArray" 
          :key="note.id"
          class="card" 
          :style="{backgroundColor: note.backgroundColor}"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{note.date}}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
  import {ref} from "vue";

  const showModal = ref(false);
  const newNote = ref("");
  const notesArray = ref([]);

  function randomBrightColor() {
    return "hsla(" + (Math.random() * 360) + ", 87%, 70%, 0.7)";
  } 

  const addNote = () => {

    if(newNote.value === ""){
      alert("empty note");
    }
    else
    {
      notesArray.value.push({
        id: Math.floor(Math.random()*100000),
        text: newNote.value,
        date: new Date().toLocaleString('sr-SP'),
        backgroundColor: randomBrightColor() 
      })

      showModal.value = false;
      newNote.value = "";
    }
  }

</script>

<style scoped>
  main{
    height: 100vh;
    width: 100vw;
  }

  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
  }
  
  .card{
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }

  .main-text{
    font-size: 14px;
  }

  .date{
    font-size: 13px;
    font-weight: bold;
  }

  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }

  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.45);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: darkgreen;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }

  .modal .close{
    background-color: crimson;
    margin-top: 7px;
  }

  textarea{
    resize: vertical;
  }

</style>