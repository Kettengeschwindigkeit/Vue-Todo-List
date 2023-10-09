<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr>
    <Loader v-if="loading" />
    <TodoList v-else-if="filterTodos.length" v-bind:todos="filterTodos" @remove-todo="removeTodo" />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import AddTodo from '@/components/AddTodo'
import TodoList from '@/components/TodoList'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [
        // { id: 1, title: "Купить хлеб", completed: false },
        // { id: 2, title: "Купить масло", completed: false },
        // { id: 3, title: "Купить пиво", completed: false }
      ],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json
          this.loading = false
        }, 1000)

      })
  },
  watch: {
    filter(value) {
      console.log(value)
    }
  },
  computed: {
    filterTodos() {
      if (this.filter === 'all') {
        return this.todos
      }

      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }

      if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo)
    },
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    }
  },
  components: {
    TodoList, AddTodo, Loader
  }
}
</script>
