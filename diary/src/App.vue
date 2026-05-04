<script setup>
  import { ref } from "vue";
  import DiaryForm from "./components/DiaryForm.vue";
  import DiaryList from "./components/DiaryList.vue";

  const posts = ref([]);

  /* för att visa ett nytt inlägg från formuläret */
  function addPost(post) {
    posts.value.push(post);
    console.log("Alla inlägg:", posts.value); /* skriver ut alla inlägg i konsolen */
  }
</script>

<template>
  <main>
    <h1>Min Dagbok</h1>
  
    <DiaryForm @add-post="addPost"/> <!-- formulär-komponent, triggas med addpost -->
  
    <DiaryList :posts="posts"/> <!-- list-komponent, parent skickar post data till DiaryList (child) -->
  </main>
</template>

<style scoped>
  main {
    max-width: 500px;
    margin: 0 auto;
    padding: 60px;
    font-family: Arial, sans-serif;
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
