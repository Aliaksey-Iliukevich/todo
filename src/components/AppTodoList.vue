<template>
    <ul class="todo-list">
        <app-todo-item
          v-for="todo in todos" 
          :key="todo.id" 
          :todo="todo"
          @toggle-todo="toggleTodo"
          @remove-todo="removeTodo"
          />
    </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import {Todo} from '../types/Todo'

export default defineComponent({
  props: {
    todos: {
      type: Array as PropType<Todo[]>,

    }
  },
  emits: {
    toggleTodo: (id: number | undefined) => Number.isInteger(id),
    removeTodo: (id: number | undefined) => Number.isInteger(id)
  },
  components: {
    AppTodoItem
  },
  methods: {
    toggleTodo(id: number | undefined) {
      this.$emit('toggleTodo', id)
    },
    removeTodo(id: number | undefined) {
      this.$emit('removeTodo', id)
    }
  }
})
</script>