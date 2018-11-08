<template>
  <div class="todo-list">
		<to-do-input class='input'></to-do-input>
		<span class="tip"><i class="fas fa-lightbulb" style="padding: 5px"></i><strong>Tip: </strong> to edit a Todo, click on the text, add stuff and press <strong>Enter</strong>. Changed your mind? Press <strong>Esc</strong>.</span>
		<div class='todo-items undone'>
			<p class="list-title">Not Done</p>
			<div class="list-items">
				<to-do-item
					v-for="todo in undoneTodos"
					:key="todo.createdAt.getTime()"
					:todo="todo"
					:now="now"
					@remove="removeTodo">
				</to-do-item>
			</div>
		</div>
		<div class='todo-items done'>
			<p class="list-title">Done</p>
			<div class="list-items">
				<to-do-item
					v-for="todo in doneTodos"
					:key="todo.createdAt.getTime()"
					:todo="todo"
					:now="now"
					@remove="removeTodo">
				</to-do-item>
			</div>
		</div>
	</div>
</template>

<script>
import ToDoInput from './ToDoInput'
import ToDoItem from './ToDoItem'
import { mapGetters } from 'vuex'

export default {
  name: 'ToDoList',
  components: { ToDoInput, ToDoItem },
  data () {
    return {
      now: Date
    }
  },
  computed: {
    ...mapGetters(['doneTodos', 'undoneTodos']),
    doneTodos () {
      return this.$store.getters.doneTodos
    },
    undoneTodos () {
      return this.$store.getters.undoneTodos
    }
  },
  created () {
    setInterval(this.updateCurrentTime, 1000 * 60)
  },
  destroyed () {
    clearInterval(this.updateCurrentTime)
  },
  methods: {
    updateCurrentTime () {
      this.now = Date.now()
    },
    removeTodo (createdAt) {
      this.$store.dispatch('removeTodo', createdAt)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
	.todo-items
		margin: auto
		margin-top 20px
		display flex
		flex-direction column
		text-align left
		background-color rgb(250, 250, 250)
		max-width: 624px
		margin-bottom 10px
		padding 0 12px
	
	.list-title
		text-align center

	.list-items
		max-height 230px
		overflow auto
	
	.input
		max-width 624px
		margin auto
		margin-bottom 10px
	
	.tip
		font-size 14px
	
</style>
