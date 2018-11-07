<template>
  <div class="todo-item">

    <input type='checkbox' v-model="todo.checked">
     {{this.todo.text}}
     <span class='timeago'> - {{ timeAgo }}</span>
  </div>
</template>

<script>
import timeAgo from '../helpers/time-ago'

export default {
  name: 'ToDoItem',
  props: {
    todo: {
      required: true
    },
    now: {}
  },
  computed: {
    timeAgo () {
      let currentDate = this.now
      return timeAgo(this.todo.createdAt)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
    .todo-item {
        padding 12px 0
    }
    .timeago {
        opacity .5
        font-size .8em
        font-weight 200
    }
</style>
