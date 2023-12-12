<script setup>
import { Icon } from "@iconify/vue";
</script>

<template>
  <main>
    <h1>About</h1>
    <p>Basic todo list application built using the Vue.js framework.</p>
    <div class="links">
      <a href="https://vuejs.org/" target="_blank" rel="noopener">
        <Icon icon="logos:vue" width="30" />
      </a>
      <a
        href="https://github.com/kevindmorris/vue-todo"
        target="_blank"
        rel="noopener"
      >
        <Icon icon="logos:github-icon" width="30" />
      </a>
      <a
        href="https://www.youtube.com/watch?v=KTFH4P8unUQ&t=5306s"
        target="_blank"
        rel="noopener"
      >
        <Icon icon="logos:youtube-icon" width="30" />
      </a>
    </div>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1,
  p {
    margin-bottom: 16px;
    text-align: center;
  }

  .links {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  a {
    margin: 0 0.25rem;
    text-decoration: none;
    color: black;
  }
}
</style>
