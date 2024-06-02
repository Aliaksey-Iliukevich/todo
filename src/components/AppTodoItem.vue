<template>
     <li class="todo-item" :class="{'todo-item--done': todo?.completed}" @click="toggleTodo">
          <div class="todo-item__status">
            <i class="bi bi-check2"></i>
          </div>
          <span class="todo-item__text">{{ todo?.text }}</span>
          <button class="todo-item__remove-button" @click.stop="removeTodo">
            <i class="bi bi-trash3"></i>
          </button>
        </li>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import {Todo} from '../types/Todo'

export default defineComponent({
    props: {
        todo: {
            type: Object as PropType<Todo>,
            requrid: true
        }
    },

    emits: {
      toggleTodo: (id: number | undefined) => Number.isInteger(id),
      removeTodo: (id: number | undefined) => Number.isInteger(id)
    },
    methods: {
      toggleTodo() {
        this.$emit('toggleTodo', this.todo?.id);
      },
      removeTodo() {
        this.$emit('removeTodo', this.todo?.id);
      }
    }
})
</script>