<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
      <input type="checkbox">
      <strong>{{ todo.id }}</strong>
      {{ todo.title }}
    </span>
    <button class="rm">&times;</button>
  </li>
</template>

<script>
  export default {
    props: {
      todo: {
        type: Object,
        required: true
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
