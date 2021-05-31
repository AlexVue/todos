<template>
  <div class="todos-wrapper">
    <todo-form @addTodo="addTodo"/>
    <todo-list
      :todo-list="todoList"
      @deleteTodo="deleteTodo"
      @setDone="setDone"
    />
  </div>
</template>

<script lang="ts">
import TodoForm from '@/components/TodoForm.vue'
import TodoList from '@/components/TodoList.vue'
import ITodoItem from '@/types/ITodoItem'
import { defineComponent, ref } from 'vue'

export default defineComponent({
  components: {
    TodoForm,
    TodoList
  },
  setup () {
    const todoList = ref<Array<ITodoItem>>([])

    const addTodo = (newTodo: ITodoItem): void => {
      todoList.value.push(newTodo)
    }

    const deleteTodo = (id: number): void => {
      todoList.value = todoList.value.filter(item => item.id !== id)
    }

    const setDone = (id: number): void => {
      todoList.value.forEach(item => {
        if (item.id === id) {
          item.done = !item.done
        }
      })
    }

    return {
      addTodo,
      deleteTodo,
      setDone,
      todoList
    }
  }
})
</script>

<style lang="scss">
.todos-wrapper {
  max-width: 560px;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
