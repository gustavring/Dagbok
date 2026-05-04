<script setup>
  import { ref, computed, onMounted, watch } from "vue";
  import DiaryForm from "./components/DiaryForm.vue";
  import DiaryList from "./components/DiaryList.vue";

  const posts = ref([]);
  const showForm = ref(false);

  onMounted(() => {
    const savedPosts = localStorage.getItem("diaryPosts");

    if (savedPosts) {
      posts.value = JSON.parse(savedPosts);
    }
  });

  watch(posts, () => {
    localStorage.setItem("diaryPosts", JSON.stringify(posts.value));
  }, { deep: true });

  const sortedPosts = computed(() => {
    return [...posts.value].sort((a, b) => {
      return new Date(b.date) - new Date(a.date);
    });
  }); 

  /* för att visa ett nytt inlägg från formuläret */
  function addPost(post) {
    posts.value.push({
      id: Date.now(),
      ...post
    });

    console.log("Alla inlägg:", posts.value); /* skriver ut alla inlägg i konsolen */
  }

  function deletePost(id) {
    posts.value = posts.value.filter(post => post.id !== id);
  }
</script>

<template>
  <main>
    <h1>Min Dagbok</h1>

    <div class="button-wrapper">
      <button @click="showForm = !showForm" :class="{ open: showForm }">
        {{ showForm ? "Stäng formulär" : "Skriv nytt inlägg" }}
      </button>
    </div>
  
    <DiaryForm v-if="showForm" @add-post="addPost"/> <!-- formulär-komponent, triggas med addpost -->
  
    <DiaryList :posts="sortedPosts" @delete-post="deletePost"/> <!-- list-komponent, parent skickar post data till DiaryList (child) -->
  </main>
</template>

<style scoped>
  main {
    max-width: 500px;
    margin: 0 auto;
    padding: 60px;
    font-family: Arial, sans-serif;
  }

  .button-wrapper {
    display: flex;
    justify-content: center;
  }

  button {
    padding: 10px;
    background: #2f4b80;
    color: white;
    border: none;
    border-radius: 7px;
    cursor: pointer;
    transition: 0.2s ease;
  }

  button.open {
    border-radius: 7px 7px 0 0;
  }

  button:hover {
    background: #34528b;
  }

  button:active {
    background: #253b64;
  }

  h1 {
    text-align: center;
    margin-bottom: 20px;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    font-size: 40px;
    font-weight: 100;
    color: rgb(255, 255, 255);
  }
</style>
