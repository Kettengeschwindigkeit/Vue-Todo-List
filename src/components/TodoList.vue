<template>
  <div>
    <ul>
      {{ todos }}
      <TodoItem />
    </ul>
  </div>
</template>

<script>
  import TodoItem from '@/components/TodoItem.vue'
  export default {
    props: ['todos'],
    components: {
      TodoItem
    }
  }
</script>
