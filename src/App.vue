<template>
   <app-header/>

   <app-filters/>

    <main class="app-main">
      <app-todo-list :todos="todos" @toggle-todo="toggleTodo" @remove-todo="removeTodo"/>

     <app-add-todo @add-todo="addTodo"/>
    </main>

    <app-footer/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppHeader from './components/AppHeader.vue'
import AppFilters from './components/AppFilters.vue'
import AppTodoList from './components/AppTodoList.vue'
import AppAddTodo from './components/AppAddTodo.vue'
import AppFooter from './components/AppFooter.vue'
import { Todo } from './types/Todo';

interface State {
  todos: Todo[]
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
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
    addTodo(todo: Todo) {
      this.todos.push(todo)
    },
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