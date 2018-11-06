<template>
  <div class="home">
      <h1>To Do App</h1>
      <to-do-list></to-do-list>
  </div>
</template>

<script>

import ToDoList from '@/components/ToDoList.vue'
export default {
  name: 'home',
  components: {
    ToDoList
  }
}
</script>
