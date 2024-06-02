<template>
   <app-header/>

   <app-filters 
    :activeFilter="activeFilter" 
    @setFilter="setFilter"/>

    <main class="app-main">
      <app-todo-list 
        :todos="filteredTodos" 
        @toggle-todo="toggleTodo" 
        @remove-todo="removeTodo"/>

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
import { Filter } from './types/Filter'

interface State {
  todos: Todo[],
  activeFilter: Filter
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.todos.filter(todo => !todo.completed)
        case 'Done':
          return this.todos.filter(todo => todo.completed)
        case 'All':
        default:
        return this.todos
      }
    }
  },
  data() : State {
    return {
      todos: [
        {id: 0, text: 'Learn the basics of Vue', completed: true},
        {id: 1, text: 'Learn the basics of Typescript', completed: false},
        {id: 2, text: 'Subscribe to the channel', completed: false},
        {id: 3, text: 'Learn the basics of HTML', completed: false},
      ],
      activeFilter: 'All'
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
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter
    }
  }
})
</script>