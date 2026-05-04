<script setup>
  defineProps({
    posts: Array
  });

  const emit = defineEmits(["delete-post"]);
</script>

<template>
  <hr>
  <section>
    <h2>Inlägg</h2>

    <p class="no-posts" v-if="posts.length === 0">Inga inlägg finns ännu</p> <!-- om listan är tom -->

    <article v-for="post in posts" :key="post.title"> <!-- loopar igenom alla inlägg -->
      <div class="post-header">
        <h3>{{ post.title }}</h3>

        <button class="delete-btn" @click="emit('delete-post', post.id)">
          ⨯
        </button>
      </div>
      <p>{{ post.date }}</p>
      <p>{{ post.text }}</p>
      <hr />
    </article>
  </section>
</template>

<style scoped>
  section {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }

  .post-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: aquamarine;
  }

  .delete-btn {
    background: transparent;
    border: none;
    cursor: pointer;
    padding: none;
    font-size: 26px;
    color: rgb(170, 11, 11);
  }

  .delete-btn:hover {
    color: rgb(206, 15, 15);
    transform: scale(1.1);
  }

  .delete-btn:active {
    color: rgb(102, 6, 6);
    transform: scale(0.9);
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
    background: #f7f7f7;
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