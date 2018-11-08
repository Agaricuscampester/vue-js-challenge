<template>
  <div class="todo-item">

    <input class="item-checkbox" type='checkbox' v-model="todo.checked">
    <input
      class="edit-field"
      type="text"
      ref="edit"
      v-model="todo.text"
      v-if="editEnabled"
      @keyup.enter="saveUpdate(todo.createdAt)"
      @keyup.esc="cancelUpdate(todo.createdAt)"
      @blur="cancelUpdate(todo.createdAt)"
    >
    <span v-if="!editEnabled" @click="updateTodo(todo.createdAt)">{{this.todo.text}}</span>
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
  data () {
    return {
      editEnabled: false,
      todoText: ''
    }
  },
  computed: {
    timeAgo () {
      let currentDate = this.now
      return timeAgo(this.todo.createdAt)
    }
  },
  methods: {
    removeTodo (createdAt) {
      this.$emit('remove', createdAt)
    },
    updateTodo (createdAt) {
      this.todoText = this.todo.text
      this.editEnabled = true
      this.$nextTick(() => this.$refs.edit.focus())
    },
    saveUpdate (createdAt) {
      this.todoText = this.todo.text
      this.editEnabled = false
    },
    cancelUpdate (createdAt) {
      this.todo.text = this.todoText
      this.editEnabled = false
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
    .edit-field {
        background-color #fafafa
        outline none
        border none
        font inherit
        width 50%
        margin-left 10px
    }
    .item-checkbox {
        margin-right 10px
    }
</style>
