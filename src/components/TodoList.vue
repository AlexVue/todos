<template>
  <div class="list-wrapper">
    <ul v-if="todoList.length">
      <li v-for="todoItem in todoList" :key="todoItem.id">
        <TodoItem
          :todoItem="todoItem"
          @deleteTodo="$emit('deleteTodo', todoItem.id)"
          @setDone="$emit('setDone', todoItem.id)"
        />
      </li>
    </ul>
    <div v-else>No todo data!</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import TodoItem from '@/components/TodoItem.vue'
import ITodoItem from '@/types/ITodoItem'

export default defineComponent({
  name: 'TodoList',
  props: {
    todoList: {
      type: Array as PropType<Array<ITodoItem>>,
      default: () => []
    }
  },
  components: {
    TodoItem
  }
})
</script>

<style scoped lang="scss">
.list-wrapper {
  width: 100%;
  margin-top: 20px;
  max-width: 380px;
  text-align: center;
  ul {
    padding: 0;
    margin: 0;
  }
  li {
    list-style: none;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 5px;
  }
}
</style>
