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
import { defineComponent } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import {Todo} from '../types/Todo'

interface State {
  todos: Todo[]
}

export default defineComponent({
  components: {
    AppTodoItem
  },
  data() : State {
    return {
      todos: [
        {id: 0, text: 'Learn the basics of Vue', completed: true},
        {id: 1, text: 'Learn the basics of Typescript', completed: false},
        {id: 2, text: 'Subscribe to the channel', completed: false},
        {id: 3, text: 'Learn the basics of HTML', completed: false},
      ]
    }
  },
  methods: {
    toggleTodo(id: number | undefined) {
      const targetTodo = this.todos.find(todo => todo.id === id);

      if(targetTodo){
        targetTodo.completed = !targetTodo.completed;
      }
    },
    removeTodo(id: number | undefined) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    }
  }
})
</script>