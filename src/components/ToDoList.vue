<template>
    <div class="todo-list">

        <to-do-input class='input'></to-do-input>

        <div class='todo-items'>
            <p class="list-title">Not Done</p>
            <div class="list-items">
                <to-do-item v-for="todo in $store.state.todos" :key="todo.createdAt.getTime()" :todo="todo"></to-do-item>
            </div>
        </div>
        <div class='todo-items done'>
            <p class="list-title">Done</p>
            <div class="list-items">
                <to-do-item v-for="todo in $store.state.todos" :key="todo.createdAt.getTime()" :todo="todo"></to-do-item>
            </div>
        </div>
    </div>
</template>

<script>
import ToDoInput from './ToDoInput'
import ToDoItem from './ToDoItem'
export default {
  name: 'ToDoList',
  components: {ToDoInput, ToDoItem}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
    .todo-items {
        margin: auto
        margin-top 30px
        display flex
        flex-direction column
        text-align left
        background-color rgb(250, 250, 250)
        max-width: 624px
        margin-bottom 10px
        padding 0 12px
    }

    .list-title {
        text-align center
    }

    .list-items {
        max-height 230px
        overflow auto
    }

    .input {
        max-width 624px
        margin auto
    }
</style>
