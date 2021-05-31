<template>
    <input type="checkbox" @change="setDone(todoItem.id)"/>
    <div :class="{'done': todoItem.done}">{{todoItem.text}}</div>
    <button
      type="button"
      class="btn-delete"
      @click="deleteTodo(todoItem.id)"
      :disabled="!todoItem.done"
    >
      <span>x</span>
    </button>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import ITodoItem from '@/types/ITodoItem'

export default defineComponent({
  name: 'TodoItem',
  emits: ['deleteTodo', 'setDone'],
  props: {
    todoItem: {
      type: Object as PropType<ITodoItem>,
      required: true
    }
  },
  setup (props, { emit }) {
    const deleteTodo = (id: number): void => {
      emit('deleteTodo', id)
    }

    const setDone = (id: number): void => {
      emit('setDone', id)
    }

    return {
      deleteTodo,
      setDone
    }
  }
})
</script>

<style scoped lang="scss">
.done {
  text-decoration: line-through;
}
.btn-delete {
  background: tomato;
  border: 1px solid tomato;
  border-radius: 4px;
  display: flex;
  justify-content: center;
  align-items: center;
  span {
    color: #FFFFFF;
  }
  &:hover {
    cursor: pointer;
  }
}
</style>
