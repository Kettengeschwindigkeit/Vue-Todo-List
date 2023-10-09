<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed">
      <strong>{{ index + 1 }}</strong>
      {{ todo.title | uppercase }}
    </span>
    <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
  export default {
    props: {
      todo: {
        type: Object,
        required: true
      },
      index: Number
    },
    filters: {
      uppercase(value) {
        return value.toUpperCase()
      }
    }
  }
</script>

<style scoped>
  li {
    display: flex;
    justify-content: space-between;
    margin-bottom: 1rem;
    padding: .5rem 2rem;
    border: 1px solid #ccc;
  }

  input {
    margin-right: 1rem;
  }

  .rm {
    font-weight: bold;
    color: #fff;
    background: red;
    border-radius: 50%;
  }

  .done {
    text-decoration: line-through;
  }
</style>
