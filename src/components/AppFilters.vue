<template>
     <aside class="app-filters">
      <section class="toggle-group">
        <button
          class="button" 
          :class="{'button--primary': activeFilter === filter}"
          v-for="filter in filters"
          :key="filter"
          @click="setFilter(filter)"
        >
          {{ filter }}
        </button>
      </section>
    </aside>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import { Filter } from '../types/Filter'

interface State {
  filters: Filter[]
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
      required: true
    }
  },
  emits: {
    setFilter: (filter: Filter) => filter
  },
  data(): State {
    return{
      filters: ['All', 'Active', 'Done']
    }
  },
  methods: {
    setFilter(filter: Filter) {
      this.$emit('setFilter', filter)
    }
  }
})
</script>