<template>
  <div class="todo-form">
    <form @submit.prevent="addTodo">
      <input
        type="text"
        placeholder="Enter todo text"
        v-model="todoText"
      />
      <button
        type="submit"
        class="todo-form__submit"
      >Add Todo</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import ITodoItem from '@/types/ITodoItem'

export default defineComponent({
  name: 'TodoForm',
  emits: [
    'addTodo'
  ],
  setup (props, { emit }) {
    const todoText = ref<string>('')

    const addTodo = (): void => {
      if (todoText.value) {
        const newTodo = {
          id: Date.now(),
          text: todoText.value,
          done: false
        } as ITodoItem

        emit('addTodo', newTodo)

        todoText.value = ''
      }
    }

    return {
      todoText,
      addTodo
    }
  }
})
</script>

<style scoped lang="scss">
.todo-form {
  width: 100%;
    form {
      width: inherit;
      display: inline-flex;
      justify-content: center;
      align-items: center;
    }
    input {
      background: #FFFFFF;
      border: 1px solid #E3E3E8;
      box-sizing: border-box;
      border-radius: 24px;
      height: 28px;
      margin-right: 10px;
      max-width: 300px;
      width: 100%;
    }
    input::placeholder {
      font-size: 14px;
      line-height: 22px;
      display: flex;
      align-items: center;
      color: #8F93A3;
      position: relative;
      left: 10px;
    }
    input:focus {
      outline: none;
      padding-left: 20px;
    }
    &__submit {
      background: tomato;
      outline: none;
      border: 1px solid tomato;
      border-radius: 24px;
      color: #FFFFFF;
      height: 28px;
      &:hover {
        cursor: pointer;
      }
    }
}
</style>
