<script setup>
  defineProps({
    posts: Array
  });
</script>

<template>
  <section>
    <h2>Inlägg</h2>

    <p class="no-posts" v-if="posts.length === 0">Inga inlägg finns ännu</p> <!-- om listan är tom -->

    <article v-for="post in posts" :key="post.title"> <!-- loopar igenom alla inlägg -->
      <h3>{{ post.title }}</h3>
      <p>{{ post.date }}</p>
      <p>{{ post.text }}</p>
      <hr /> <!-- linje mellan alla inlägg -->
    </article>
  </section>
</template>

<style scoped>
  section {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }

  h2 {
    color: rgb(255, 255, 255);
    text-align: center;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    font-weight: 100;
    font-size: 30px;
    margin: 20px 0 10px 0;
  }

  article {
    background: #e3e3e4;
    padding: 15px;
    border-radius: 8px;

    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  }

  h3 {
    margin: 0;
    color: rgb(36, 36, 36);
  }

  p {
    margin: 5px 0;
    color: rgb(65, 65, 65);
  }

  .no-posts {
    color: rgb(255, 255, 255);
    font-size: 20px;
    text-align: center;
  }

  hr {
    margin-top: 10px;
    border: none;
    border-top: 1px solid #ddd;
  }
</style>