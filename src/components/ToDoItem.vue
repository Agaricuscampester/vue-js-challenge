<template>
  <div class="todo-item">

    <input type='checkbox' v-model="todo.checked">
     {{this.todo.text}}
     <span class='timeago'> - {{ timeAgo }}</span>
     <button class="delete-button" @click="removeTodo(todo.createdAt)">
       <i class="fas fa-trash"></i>
    </button>
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
  },
  methods: {
    removeTodo(createdAt) {
      this.$emit('remove', createdAt)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
    .todo-item {
        padding 20px 0
        border-top 1px lightgray dashed
        position relative
    }
    .timeago {
        opacity .5
        font-size .8em
        font-weight 200
    }
    .delete-button {
        background-color #fafafa
        color #B22222
        border none
        padding 5px
        padding-top 0
        font inherit
        cursor pointer
        position absolute
        right 10px
        outline none
    }
</style>
